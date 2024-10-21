# EX-NO-9---RSA-Encryption-Algorithm
# Aim:
The aim of this project is to implement the RSA encryption and decryption algorithm in C, demonstrating the fundamental principles of public-key cryptography. The program generates a public-private key pair, encrypts a plaintext message using the public key, and decrypts the corresponding ciphertext using the private key.

# Algorithm:

1. Select two large prime numbers p and q.
2. Compute n = p * q.
3. Calculate Euler's Totient function: φ(n) = (p-1) * (q-1).
4. Choose an integer e such that 1 < e < φ(n) and gcd(e, φ(n)) = 1.
5. Determine the private key d such that (d * e) % φ(n) = 1.

# Encryption:
Represent the message M as an integer within the range [0, n-1].
Compute the ciphertext C using the formula: C = M^e % n.

# Decryption:
Retrieve the original message M using the private key d with the formula: M = C^d % n.

# Program:
```
#include <stdio.h>
#include <math.h>

// Function to compute greatest common divisor (GCD)
int gcd(int a, int b) {
    if (b == 0)
        return a;
    else
        return gcd(b, a % b);
}

// Function to compute power (base^exp) % mod
long long int mod_pow(int base, int exp, int mod) {
    long long int result = 1;
    while (exp > 0) {
        if (exp % 2 == 1)
            result = (result * base) % mod;
        base = (base * base) % mod;
        exp /= 2;
    }
    return result;
}

// Function to perform RSA encryption
long long int encrypt(int msg, int e, int n) {
    return mod_pow(msg, e, n);
}

// Function to perform RSA decryption
long long int decrypt(int cipher, int d, int n) {
    return mod_pow(cipher, d, n);
}

int main() {
    // Step 1: Two prime numbers (p, q)
    int p = 61;
    int q = 53;

    // Step 2: Compute n = p * q
    int n = p * q;

    // Step 3: Compute Euler's Totient Function, φ(n) = (p-1) * (q-1)
    int phi = (p - 1) * (q - 1);

    // Step 4: Choose public key exponent e such that 1 < e < φ(n) and gcd(e, φ(n)) = 1
    int e = 17;  // A small prime number, commonly used

    // Step 5: Compute private key exponent d such that (d * e) % φ(n) = 1
    int d = 0;
    for (int i = 1; i < phi; i++) {
        if ((e * i) % phi == 1) {
            d = i;
            break;
        }
    }

    // Display public and private keys
    printf("Public Key (e, n) = (%d, %d)\n", e, n);
    printf("Private Key (d, n) = (%d, %d)\n", d, n);

    // Message to be encrypted
    int msg = 42; // Plain text message

    // Step 6: Encrypt the message
    long long int cipher = encrypt(msg, e, n);
    printf("Encrypted Message: %lld\n", cipher);

    // Step 7: Decrypt the message
    long long int decrypted_msg = decrypt(cipher, d, n);
    printf("Decrypted Message: %lld\n", decrypted_msg);

    return 0;
}

```
# OUTPUT:
![image](https://github.com/user-attachments/assets/70911441-8ca1-4665-b344-0a996cd32a8a)

# Result:
The program successfully encrypts a plaintext message using the RSA algorithm and decrypts it back to the original message.
