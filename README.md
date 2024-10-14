# Cesar
import random

class CesarCipher:
    def __init__(self, shift):
        self.shift = shift

    def encrypt(self, plaintext):
        result = ''
        for char in plaintext:
            if char.isalpha():
                shift = self.shift % 26
                new_char = chr((ord(char.lower()) - 97 + shift) % 26 + 97)
                result += new_char.upper() if char.isupper() else new_char
            else:
                result += char
        return result

    def decrypt(self, ciphertext):
        result = ''
        for char in ciphertext:
            if char.isalpha():
                shift = self.shift % 26
                new_char = chr((ord(char.lower()) - 97 - shift) % 26 + 97)
                result += new_char.upper() if char.isupper() else new_char
            else:
                result += char
        return result

def generate_verification_code():
    """Genera un código de verificación aleatorio de 6 dígitos"""
    return str(random.randint(100000, 999999))

def login():
    # Primera fase de autenticación: Usuario y contraseña
    username = input("Enter your username: ")
    password = input("Enter your password: ")

    # Aquí se puede implementar lógica para verificar credenciales (ej: base de datos)
    if username == "sofiaalu" and password == "galletas":
        print("Login successful!")

        # Segunda fase de autenticación: Código de verificación
        verification_code = generate_verification_code()
        print(f"A verification code has been sent: {verification_code}")
        user_code = input("Enter the verification code: ")

        if user_code == verification_code:
            print("Two-step verification successful!")
            return True
        else:
            print("Invalid verification code. Access denied.")
            return False
    else:
        print("Invalid username or password.")
        return False

def cesar_menu():
    while True:
        shift_input = input("Enter shift value for Caesar Cipher (a number): ")
        if shift_input.isdigit():
            shift = int(shift_input)
            break
        else:
            print("Invalid input! Please enter a valid number.")

    cesar = CesarCipher(shift)

    choice = input("Do you want to (e)ncrypt or (d)ecrypt? ").lower()
    if choice == 'e':
        plaintext = input("Enter the text to encrypt: ")
        print(f"Encrypted Text: {cesar.encrypt(plaintext)}")
    elif choice == 'd':
        ciphertext = input("Enter the text to decrypt: ")
        print(f"Decrypted Text: {cesar.decrypt(ciphertext)}")
    else:
        print("Invalid option!")

if __name__ == "__main__":
    if login():  # Solo accede al menú si pasa las dos fases de autenticación
        cesar_menu()
