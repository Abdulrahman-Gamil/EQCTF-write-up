## **Neighbour-RSA Challenge**

The challenge, titled "neighbour-rsa," revolves around a cryptographic scenario where the RSA modulus \( N \) is generated using two prime numbers \( p \) and \( q \), with \( q \) being the 5000th next prime after \( p \). The goal is to decrypt a ciphertext \( C \) to recover the original flag. The challenge provides the public key \( (N, e) \) and the ciphertext \( C \), along with a Python script that generates these values.

#### **Given Code**


```python
from Crypto.Util.number import *
from gmpy2 import next_prime

def loop_next_prime(p):
	for i in range(5000):
		p = next_prime(p)
	q = p
	return q

flag = b"EQCTF{<REDACTED>}"

p = getPrime(1024)
q = loop_next_prime(p)

N = int(p*q)
e = 65537

C = pow(bytes_to_long(flag),e,N)

print(f"{N=}")
print(f"{e=}")
print(f"{C=}")

# N=14587704432822344892341272427282646120364434437414523883376089608218979364959927948590898540264210246449374363014541914863792835772986609660515612532877044074684115597786182642011407163350289201826895454398548254854919237599957739718174053771619150887665707867636064460914489445835497948439951659044458159773886454887057327846897569977945202458245268351728125973721764332352011029125694046428350269451464778793326007087955043888570293765138721335344787054343738337660927131968049415376352589981259058448540690666004751490375493430556965591293772542601776934892741235532054785639594081598607404023545471998403197674267
# e=65537
# C=7329184746351979600304810893726842767688467204256990201181172159445966473650977905122553415838916142690364388789400790015517642902297387406215773278164829517035052625373870964570981590734714495297149889660019174034119566329569798047522829383224123884562703447321306836996392334132844673471179765556339187200820259655159008340673516040862000226792914228312336356120448967504158288031247387263438925257977725844911872753683719735641011693324441777888582417108481882731436005780409094974241968759397096299213838515746566064813787517925040756180508206242396925444425306180593790729890681708626826056328684043890127100581
```

The script generates a 1024-bit prime \( p \), computes \( q \) as the 5000th next prime after \( p \), and then calculates the RSA modulus \( N = p \times q \). The public exponent \( e \) is set to 65537, and the flag is encrypted using RSA encryption to produce the ciphertext \( C \).

#### **Understanding the Vulnerability**

The vulnerability in this challenge lies in the way \( q \) is generated. Since \( q \) is the 5000th next prime after \( p \), the difference between \( p \) and \( q \) is relatively small compared to the size of \( p \) and \( q \) themselves. This makes \( N \) susceptible to factorization using Fermat's factorization method, which is efficient when the two prime factors are close to each other.

#### **Solution Approach**

To solve this challenge, we can use Fermat's factorization method to factorize \( N \) into \( p \) and \( q \). Once we have \( p \) and \( q \), we can compute the private exponent \( d \) and decrypt the ciphertext \( C \) to recover the flag.

#### **Solution Code**

The following Python script implements the solution:

```python
import math
def is_perfect_square(n):
    root = int(math.isqrt(n))
    return root * root == n

def fermat_factorization(N):
    a = math.isqrt(N) + 1
    while True:
        b_squared = a * a - N
        if b_squared < 0:
            a = math.isqrt(N) + 1
            b_squared = a * a - N
        if is_perfect_square(b_squared):
            b = int(math.isqrt(b_squared))
            p = a - b
            q = a + b
            return p, q
        a += 1

# Given N, e, and C
N = 14587704432822344892341272427282646120364434437414523883376089608218979364959927948590898540264210246449374363014541914863792835772986609660515612532877044074684115597786182642011407163350289201826895454398548254854919237599957739718174053771619150887665707867636064460914489445835497948439951659044458159773886454887057327846897569977945202458245268351728125973721764332352011029125694046428350269451464778793326007087955043888570293765138721335344787054343738337660927131968049415376352589981259058448540690666004751490375493430556965591293772542601776934892741235532054785639594081598607404023545471998403197674267
e = 65537
C = 7329184746351979600304810893726842767688467204256990201181172159445966473650977905122553415838916142690364388789400790015517642902297387406215773278164829517035052625373870964570981590734714495297149889660019174034119566329569798047522829383224123884562703447321306836996392334132844673471179765556339187200820259655159008340673516040862000226792914228312336356120448967504158288031247387263438925257977725844911872753683719735641011693324441777888582417108481882731436005780409094974241968759397096299213838515746566064813787517925040756180508206242396925444425306180593790729890681708626826056328684043890127100581

# Factor N using Fermat's method
p, q = fermat_factorization(N)

# Compute phi(N)
phi = (p - 1) * (q - 1)

# Compute the private exponent d
from Crypto.Util.number import inverse
d = inverse(e, phi)

# Decrypt the ciphertext C
from Crypto.Util.number import long_to_bytes
m = pow(C, d, N)
flag = long_to_bytes(m)
print(flag)
```

#### **Explanation of the Solution**

1. **Fermat's Factorization Method**:

   - The function `fermat_factorization(N)` attempts to factorize \( N \) by finding two integers \( a \) and \( b \) such that \( N = a^2 - b^2 \). This can be rewritten as \( N = (a - b)(a + b) \), where \( p = a - b \) and \( q = a + b \).
   - The method works efficiently when \( p \) and \( q \) are close to each other, which is the case in this challenge.

2. **Computing the Private Exponent \( d \)**:

   - Once \( p \) and \( q \) are known, we compute \( \phi(N) = (p - 1)(q - 1) \).
   - The private exponent \( d \) is then computed as the modular inverse of \( e \) modulo \( \phi(N) \), i.e., \( d = e^{-1} \mod \phi(N) \).

3. **Decrypting the Ciphertext**:
   - The ciphertext \( C \) is decrypted using the private exponent \( d \) to recover the plaintext \( m \): \( m = C^d \mod N \).
   - Finally, the plaintext \( m \) is converted from a long integer to a byte string, revealing the flag.


The "neighbour-rsa" challenge demonstrates the importance of proper prime generation in RSA. When the primes \( p \) and \( q \) are too close to each other, the modulus \( N \) becomes vulnerable to factorization using Fermat's method. By exploiting this vulnerability, we were able to factorize \( N \), compute the private key, and decrypt the ciphertext to recover the flag.

**Flag**: `EQCTF{<REDACTED>}` (The actual flag will be revealed when the script is executed with the correct values.)

**Flag**: `EQCTF{cla554ic_ferm4t_fact0rization_ch4llenge!!}` 






## **Neighbour-RSA-2 Challenge**

The challenge, titled "neighbour-rsa-2," is a follow-up to the previous "neighbour-rsa" challenge. This time, the RSA modulus \( N \) is generated using two primes \( p \) and \( q \), where \( q \) is the next prime after \( a + p \), and \( a \) is a large random number. The challenge provides the public key \( (N, e) \), the ciphertext \( C \), and an additional value \( f = q + a - p \). The goal is to decrypt the ciphertext \( C \) to recover the original flag.

#### **Given Code**

The provided Python script generates the RSA parameters:

```python
from Crypto.Util.number import *
from gmpy2 import prev_prime as next_prime
import secrets

flag = b"EQCTF{<REDACTED>}"
a = bytes_to_long(secrets.token_bytes(100))

p = getPrime(1024)
q = next_prime(a+p)

N = int(p*q)
e = 65537
f = int(q+a-p)

C = pow(bytes_to_long(flag),e,N)

print(f"{N=}")
print(f"{e=}")
print(f"{C=}")
print(f"{f=}")

# N=10986069679740899320769487987259965136338163538313920951921558170716399011131571749355967327929782757252961432250665732844670832757630969990974354211674665217879301194915967815961901955331119097862220567741900953344002421010199387139438258915388299120537312319419560196095221842536034797857570594271497968571543268632342368822758109031157038270115475046299925831141039892806064466450571546834222025788616070408548026473179492912530200671560292851465500255213172920644302815477881129226831758156389887396481079039150256181152083078507883863985140189407376955776873853730599843478872399976242973508423433618152961348309
# e=65537
# C=2195468989281538327484120144714886786222108443822386213335264431639447179575013802497596322014889540032797783666693430103844035492180467143334243466603968944829680836129211979667061913058333561267630828758422011805278536599370681276716534375047691415305153173304117404635308274845621779917651565487097467077938208235595083835638297185421167329868537607503750906624903899336968072524704962983010525959106240384416922803445710408493786560172567404469778095227805268385869729463091111594408973206573286013513443234182105724723290297083787222131780636442462497223002541517291130831271935451970740180808267897428166746499
# f=4203301120017181153512192371191327436380286582036247438379481982220240276670686609670968370331071343886281566516951351186472802979725501149166852576293749655990806367361286991990410689444889766967820170478115967009340001288791419622177173652
```

The script generates a 1024-bit prime \( p \), computes \( q \) as the next prime after \( a + p \), and then calculates the RSA modulus \( N = p \times q \). The public exponent \( e \) is set to 65537, and the flag is encrypted using RSA encryption to produce the ciphertext \( C \). Additionally, the value \( f = q + a - p \) is provided.

#### **Understanding the Vulnerability**

The vulnerability in this challenge lies in the relationship between \( p \), \( q \), and \( a \). Specifically, \( q \) is the next prime after \( a + p \), and \( f = q + a - p \). This relationship allows us to approximate \( a \) and use it to factorize \( N \).

#### **Solution Approach**

To solve this challenge, we can use the following steps:

1. **Approximate \( a \)**:

   - From \( f = q + a - p \), and knowing that \( q \) is close to \( a + p \), we can approximate \( a \) as \( a \approx \frac{f}{2} \).

2. **Approximate \( p \)**:

   - Using the approximation \( q \approx p + a \), we can write \( N \approx p \times (p + a) \).
   - This leads to the quadratic equation \( p^2 + a p - N \approx 0 \), which can be solved for \( p \).

3. **Find Exact \( p \) and \( q \)**:

   - Using the approximate value of \( p \), we can iteratively find the exact \( p \) and \( q \) by checking if \( p \times q = N \).

4. **Compute the Private Key \( d \)**:

   - Once \( p \) and \( q \) are known, we can compute \( \phi(N) = (p - 1)(q - 1) \) and then compute \( d = e^{-1} \mod \phi(N) \).

5. **Decrypt the Ciphertext**:
   - Finally, we can decrypt the ciphertext \( C \) using the private key \( d \) to recover the flag.

#### **Solution Code**

The following Python script implements the solution:

```python
from Crypto.Util.number import long_to_bytes
from gmpy2 import isqrt, next_prime

N = 10986069679740899320769487987259965136338163538313920951921558170716399011131571749355967327929782757252961432250665732844670832757630969990974354211674665217879301194915967815961901955331119097862220567741900953344002421010199387139438258915388299120537312319419560196095221842536034797857570594271497968571543268632342368822758109031157038270115475046299925831141039892806064466450571546834222025788616070408548026473179492912530200671560292851465500255213172920644302815477881129226831758156389887396481079039150256181152083078507883863985140189407376955776873853730599843478872399976242973508423433618152961348309
e = 65537
C = 2195468989281538327484120144714886786222108443822386213335264431639447179575013802497596322014889540032797783666693430103844035492180467143334243466603968944829680836129211979667061913058333561267630828758422011805278536599370681276716534375047691415305153173304117404635308274845621779917651565487097467077938208235595083835638297185421167329868537607503750906624903899336968072524704962983010525959106240384416922803445710408493786560172567404469778095227805268385869729463091111594408973206573286013513443234182105724723290297083787222131780636442462497223002541517291130831271935451970740180808267897428166746499
f = 4203301120017181153512192371191327436380286582036247438379481982220240276670686609670968370331071343886281566516951351186472802979725501149166852576293749655990806367361286991990410689444889766967820170478115967009340001288791419622177173652

a_approx = f // 2

discriminant = a_approx**2 + 4*N
p_approx = ( -a_approx + isqrt(discriminant) ) // 2

q_approx = N // p_approx

p = p_approx
while True:
    q_candidate = N // p
    if p * q_candidate == N:
        q = q_candidate
        break
    p = next_prime(p)

phi = (p - 1) * (q - 1)
d = pow(e, -1, phi)

flag = pow(C, d, N)
print(long_to_bytes(flag).decode())
```

#### **Explanation of the Solution**

1. **Approximate \( a \)**:

   - From \( f = q + a - p \), and knowing that \( q \) is close to \( a + p \), we approximate \( a \) as \( a \approx \frac{f}{2} \).

2. **Approximate \( p \)**:

   - Using the quadratic formula, we solve \( p^2 + a p - N \approx 0 \) to find an approximate value for \( p \).

3. **Find Exact \( p \) and \( q \)**:

   - Starting from the approximate \( p \), we iteratively find the exact \( p \) and \( q \) by checking if \( p \times q = N \).

4. **Compute the Private Key \( d \)**:

   - Once \( p \) and \( q \) are known, we compute \( \phi(N) \) and then \( d \).

5. **Decrypt the Ciphertext**:
   - Using the private key \( d \), we decrypt the ciphertext \( C \) to recover the flag.



The neighbour-rsa-2 challenge shows that sometimes, when mathematical tricks don’t work, brute-forcing can save the day. By approximating the values and iterating through possible solutions, we were able to factorize 
N
N, compute the private key, and decrypt the ciphertext to recover the flag. As the flag says: "If you can't find a solution, brute-forcing is always the key!"

**Flag**: `EQCTF{<REDACTED>}` (The actual flag will be revealed when the script is executed with the correct values.)

**Flag**: `EQCTF{if_y0u_c4nt_find_a_solution_brut3_f0rce_alw4ys_the_k3y}` 
