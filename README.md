# Python Password Manager

A simple Command-Line Interface (CLI) application designed to securely store and manage your passwords using symmetric encryption provided by the `cryptography` library.

## 🚀 Features

-   **Secure Password Storage:** Encrypts account passwords before writing them to a local file (`passwords.txt`), ensuring they are not stored in plaintext.
-   **Fernet Symmetric Encryption:** Leverages the robust Fernet implementation from the `cryptography` library, which uses AES-128 in CBC mode with HMAC for authentication.
-   **Master Password Protection:** Access to encrypted passwords is gated by a user-defined master password, adding an additional layer of security.
-   **Add and View Modes:** Allows users to easily add new account credentials or view previously stored ones.

## ⚙️ How It Works

1.  **Key Generation (Initial Setup):** A unique encryption key is generated and stored in `key.key`. This key is fundamental for encryption and decryption. *(Note: The `write_key()` function is commented out and needs to be uncommented and run once to generate this file.)*
2.  **Master Password Input:** The user provides a master password at the start of each session.
3.  **Derived Encryption Key:** The stored `key.key` is combined with the master password to derive the final encryption key used by Fernet. This means that even if `key.key` is compromised, the master password is still required to decrypt content.
4.  **Encryption:** When adding a new password, it is encrypted using the derived key and then stored alongside the account name in `passwords.txt`.
5.  **Decryption:** When viewing passwords, the application reads the encrypted data, decrypts it using the same derived key, and displays the original password.

## 🛠️ Setup and Installation

1.  **Clone the repository:**
    ```bash
    git clone [your-repository-url]
    cd [your-repository-name]
    ```
2.  **Install dependencies:**
    ```bash
    pip install cryptography
    ```
3.  **Generate the encryption key (one-time setup):**
    Uncomment the `write_key()` function in the script and run the script once. This will create the `key.key` file.
    ```python
    # Uncomment these lines in your script:
    # def write_key():
    #     key = Fernet.generate_key()
    #     with open("key.key", "wb") as key_file:
    #         key_file.write(key)
    #
    # Then run:
    # write_key() 
    # (or simply run the script after uncommenting, it will execute)
    ```
    *(Remember to re-comment `write_key()` or remove the direct call to it after the `key.key` file has been generated, to avoid overwriting your key.)*
4.  **Run the application:**
    ```bash
    python your_script_name.py
    ```

## 📝 Usage

Upon running the script, you will be prompted for a master password.
Then, choose one of the following modes:

-   `add`: To add a new account name and password.
-   `view`: To display all stored account names and their decrypted passwords.
-   `q`: To quit the application.

## ⚠️ Important Security Considerations

-   **Master Password:** The security of your stored passwords heavily relies on the strength and secrecy of your master password. Choose a strong, unique password.
-   **`key.key` File:** This file contains a crucial part of your encryption key. Treat it with the same confidentiality as your master password. Do not share it or upload it to public repositories without proper precautions (e.g., `.gitignore`).
-   **Current Implementation Note:** The current implementation appends the `master_pwd` directly to the loaded `key`. For a more robust key derivation, consider using a Key Derivation Function (KDF) like `PBKDF2HMAC` from `cryptography.hazmat.primitives.kdf.pbkdf2` to securely combine the key and master password into a Fernet-compatible key. The current method of concatenation might lead to a key that is not exactly 32 URL-safe base64-encoded bytes, which Fernet requires.

---

## 💻 Development Environment / Technical Specifications

-   **Operating System:** Windows 10
-   **Processor:** AMD Ryzen 5 3500U with Radeon Vega Mobile Gfx @ 2.10 GHz
-   **Installed RAM:** 16 GB (13.9 GB usable)
-   **Graphics Card:** AMD Radeon(TM) Vega 8 Graphics (2 GB)
-   **Python Version:** 3.x
-   **Key Libraries:** `cryptography`
