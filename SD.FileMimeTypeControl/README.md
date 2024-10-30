# File Mime Type Control Package

Bu paket ile requesten aldiginiz IFromFile dosyarinizi jpg ve png i�in type kontrol�ne tabi tutabilirsiniz.
Kontrol� byte �zerinden yapar ve eger basarisiz olursa **false** d�nd�r�r. 

## Usage
```csharp
bool checkfileForJpg = file.CheckForJpg();//basarisiz ise false d�ner.
bool checkfileForPng = file.CheckForPng();//basarisiz ise false d�ner.
```

## Resource Code
```csharp
public static class ExtensionMethods
{
    public static bool CheckForJpg(this IFormFile file)
    {
        using (var stream = new MemoryStream())
        {
            file.CopyTo(stream);
            byte[] fileBytes = stream.ToArray();
            string jpgValue =
                fileBytes[0].ToString() +
                fileBytes[1].ToString() +
                fileBytes[2].ToString();

            if (jpgValue != "255216255")
            {
                return false;
            }
        }
        return true;
    }

    public static bool CheckForPng(this IFormFile file)
    {
        using (var stream = new MemoryStream())
        {
            file.CopyTo(stream);
            byte[] fileBytes = stream.ToArray();
            string pngValue =
                fileBytes[0].ToString() +
                fileBytes[1].ToString() +
                fileBytes[2].ToString() +
                fileBytes[3].ToString();

            if (pngValue != "137807871")
            {
                return false;
            }
        }
        return true;
    }
}
```
