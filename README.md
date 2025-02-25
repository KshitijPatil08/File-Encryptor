# File-Encryptor

File Encryptor is a simple yet effective Python-based tool for encrypting and decrypting files using the Fernet symmetric encryption from the cryptography library. This ensures that sensitive data remains secure and accessible only to authorized users

This Python script is a File Encryptor that uses the Fernet encryption system from the cryptography library. Below is a detailed breakdown of how the script works.

This project uses the Fernet symmetric encryption algorithm from the cryptography library, which is based on AES (Advanced Encryption Standard) in CBC mode with PKCS7 padding.

Fernet Encryption Details
Uses AES-128 (128-bit key size) in CBC (Cipher Block Chaining) mode.
Uses PKCS7 padding to ensure block size alignment.
Generates a random IV (Initialization Vector) for each encryption.
HMAC (Hash-based Message Authentication Code) with SHA256 ensures integrity.

How It Works in Your Project
A random key (128-bit) is generated using Fernet.generate_key().
The key is stored in a file (encryption_key.key) and reused.
Data is encrypted using AES-128 in CBC mode with a new IV for each encryption.
A HMAC-SHA256 authentication tag is appended to prevent tampering.
The encrypted file can only be decrypted using the exact same key.

1️ Importing Required Library
from cryptography.fernet import Fernet
The Fernet module from cryptography.fernet is used for symmetric encryption (same key for encryption and decryption).

2️ Generating an Encryption Key
def generate_key():
    return Fernet.generate_key()
This function generates a random encryption key, which is required to encrypt and decrypt files.
The key is unique and must be stored securely.

3️ Saving and Loading the Encryption Key
def save_key(key, key_file):
    with open(key_file, 'wb') as file:
        file.write(key)
Saves the generated encryption key to a file (encryption_key.key).
It writes the key in binary mode (wb).

def load_key(key_file):
    with open(key_file, 'rb') as file:
        return file.read()
Reads and loads the encryption key from the file.
It reads the key in binary mode (rb).

4️ Encrypting a File
def encrypt_file(input_file, output_file, key):
    with open(input_file, 'rb') as file:
        data = file.read()
Opens the input file (the file you want to encrypt) in binary mode (rb) and reads its content.

    fernet = Fernet(key)
    encrypted_data = fernet.encrypt(data)
Uses Fernet(key) to create an encryption object.
Encrypts the file content (data) using .encrypt(data).

    with open(output_file, 'wb') as file:
        file.write(encrypted_data)
Saves the encrypted data to the specified output_file in binary mode (wb).

5️ Decrypting a File
def decrypt_file(input_file, output_file, key):
    with open(input_file, 'rb') as file:
        encrypted_data = file.read()
Opens the encrypted file in binary mode (rb) and reads its content.

    fernet = Fernet(key)
    decrypt_data = fernet.decrypt(encrypted_data)
Uses the same key to decrypt the encrypted data.
.decrypt(encrypted_data) restores the original file content.

    with open(output_file, 'wb') as file:
        file.write(decrypt_data)
Saves the decrypted data to the specified output_file.

6️ Running the Script

if __name__ == "__main__":
This ensures the script runs only when executed directly (not when imported as a module).

    key = generate_key()
    key_file = 'encryption_key.key'
    save_key(key, key_file)
Generates a new encryption key and saves it to encryption_key.key.

    input_file = 'plain_text.txt'
    encrypted_file = 'encrypted_file.txt'
    decrypted_file = 'decrypted_file.txt'
Specifies filenames for the original, encrypted, and decrypted files.

    encrypt_file(input_file, encrypted_file, key)
    print(f"File '{input_file}' encrypted to '{encrypted_file}'")
Calls encrypt_file() to encrypt plain_text.txt and save it as encrypted_file.txt.
Prints a message confirming encryption.

    decrypt_file(encrypted_file, decrypted_file, key)
    print(f"File '{encrypted_file}' decrypted to '{decrypted_file}'")
Calls decrypt_file() to decrypt encrypted_file.txt and save it as decrypted_file.txt.
Prints a message confirming decryption.
