# sunstealer.krypta

```code
using System.Security.Cryptography;
using System.Text;

namespace SunStealer
{
    internal class Program
    {
        static void Encrypt(string plaintext)
        {
    
            byte[] key = System.Text.Encoding.ASCII.GetBytes();
            byte[] iv = System.Text.Encoding.ASCII.GetBytes();

            using (Aes aes = Aes.Create())
            {
                aes.Key = key;
                aes.IV = iv;
                ICryptoTransform encryptor = aes.CreateEncryptor(aes.Key, aes.IV);
                byte[] encryptedBytes;
                using (var msEncrypt = new System.IO.MemoryStream())
                {
                    using (var csEncrypt = new CryptoStream(msEncrypt, encryptor, CryptoStreamMode.Write))
                    {
                        byte[] plainBytes = Encoding.UTF8.GetBytes(plaintext);
                        csEncrypt.Write(plainBytes, 0, plainBytes.Length);
                    }
                    encryptedBytes = msEncrypt.ToArray();
                }
                string encryptedText = Convert.ToBase64String(encryptedBytes);
                Console.WriteLine($"{plaintext} => {encryptedText.Substring(0, 4)} {encryptedText.Substring(3, 4)} {encryptedText.Substring(7, 4)} {encryptedText.Substring(11, 4)} {encryptedText.Substring(15, 4)} {encryptedText.Substring(19, 4)} {encryptedText.Substring(23, 4)} {encryptedText.Substring(27, 4)}");
            }
        }

        static void Main(string[] args)
        {

            Console.ReadLine();
        }
    }
}
```
