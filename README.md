# caesar-cipher-samples
class ShiftCipher:
    """
    ShiftCipher objects that can encrypt and decode text messages based on a specific shift length.
    """

    def __init__(self, shift):
        """
        Constructs a ShiftCipher for the specified degree of shift (positive or negative),
        by building a cipher (dictionary mapping from letters to other letters), and
        a decoder (the inverse of the cipher)
        """
        self.shift = shift
        self.letters = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz"
        self.cipher = {self.letters[i]: self.letters[(i+shift)%len(self.letters)] for i in range(len(self.letters))}
        self.decoder = {self.letters[i]: self.letters[(i-shift)%len(self.letters)] for i in range(len(self.letters))}

    def transform_message(self, message, cipher):
        """
        Transforms a message using the specified cipher.  Is not called by users directly,
        and can be called with either the cipher (to encrypt) or the decoder (to decode).
        """
        tmsg = ''
        for c in message:
            tmsg = tmsg + cipher.get(c, c)
        return tmsg

    def encrypt(self, message):
        """
        Transforms a message using the cipher, by calling self.transform_message
        """
        return self.transform_message(message, self.cipher)

    def decode(self, message):
        """
        Transforms a message using the decoder, by calling self.transform_message
        """
        return self.transform_message(message, self.decoder)


test = "I come to bury Caesar, not to praise him."

c0 = ShiftCipher(0)
print(c0.cipher)
m3 = ShiftCipher(-3)
print(m3.cipher)
p13 = ShiftCipher(13)
print(p13.cipher)



