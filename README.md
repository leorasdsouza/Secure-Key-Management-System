# Secure-Key-Management-System
This repository contains the implementation of a **Secure Key Management System** that handles symmetric and asymmetric encryption, key exchange, and certificate revocation. The system is designed to securely generate, distribute, and manage cryptographic keys for secure communication.

# Components
The system consists of three main components:

## Symmetric Key Distribution
- A Key Distribution Center (KDC) generates and distributes symmetric keys to clients using pre-shared keys.
- Clients decrypt the symmetric key and use it for secure communication.

## Public Key Infrastructure (PKI)
- A Certificate Authority (CA) issues and revokes digital certificates for clients.
- Clients use their certificates for secure communication and authentication.

## Diffie-Hellman Key Exchange
- Two parties securely derive a shared secret over an insecure channel.
- The shared secret is used for secure communication.

# Code Overview

## 1. Symmetric Key Distribution

### Description:
- The KDC generates symmetric keys and distributes them to clients.
- Symmetric keys are encrypted using each client's pre-shared key.
- Clients decrypt the symmetric key and use it for secure communication.

### Example Usage:
```python
kdc = KDC()
kdc.register_client("client1", os.urandom(32))  # Register client1
kdc.register_client("client2", os.urandom(32))  # Register client2

# Distribute a symmetric key between client1 and client2
encrypted_key1, encrypted_key2 = kdc.distribute_key("client1", "client2")

# Clients decrypt the symmetric key
decrypted_key1 = kdc.decrypt(encrypted_key1, kdc.client_keys["client1"])
decrypted_key2 = kdc.decrypt(encrypted_key2, kdc.client_keys["client2"])

# Verify that both clients have the same symmetric key
assert decrypted_key1 == decrypted_key2, "Decrypted keys do not match!"
``` 

## Public Key Infrastructure (PKI)

### Description:
- The Certificate Authority (CA) issues and revokes digital certificates for clients.
- Clients generate their own public-private key pairs and request certificates from the CA.
- Certificates are used for secure communication and authentication.

### Example Usage:
```python
ca = CA()
client_private_key = rsa.generate_private_key(public_exponent=65537, key_size=2048)
client_public_key = client_private_key.public_key()

# Issue a certificate for client1
client_cert = ca.issue_certificate(client_public_key, "client1")

# Revoke the certificate
ca.revoke_certificate(client_cert)
print("Is certificate revoked?", ca.is_revoked(client_cert))
``` 

## Diffie-Hellman Key Exchange

### Description:
- Two parties generate their own private and public keys using shared parameters.
- They exchange public keys and compute a shared secret.
- The shared secret is used for secure communication.

### Example Usage:
```python
# Generate DH parameters
parameters = dh.generate_parameters(generator=2, key_size=2048)

# Generate private and public keys for two parties
private_key_a = parameters.generate_private_key()
public_key_a = private_key_a.public_key()

private_key_b = parameters.generate_private_key()
public_key_b = private_key_b.public_key()

# Perform key exchange
shared_key_a = private_key_a.exchange(public_key_b)
shared_key_b = private_key_b.exchange(public_key_a)

# Verify that both parties have the same shared key
assert shared_key_a == shared_key_b, "Shared keys do not match!"
```

## How to Run the Code
Click the **"Open in Colab"** button below
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/leorasdsouza/Secure-Key-Management-System/blob/main/Secure_Key_Management_System.ipynb)

#### **Option 2: Run Locally**

1. Download the script `Secure_Key_Management_System.ipynb` from this repository.
2. Open a terminal or command prompt.
3. Run the following command:
   ```bash
   python Secure_Key_Management_System.ipynb
   ```

   
