# File Mime Type Control Package

With this package, you can type-check the **IFromFile** files you receive upon request for jpg and png. 
It checks byte and returns **false** if it fails.

## Usage
```csharp
bool checkfileForJpg = file.CheckForJpg();//If unsuccessful, it returns false.
bool checkfileForPng = file.CheckForPng();//If unsuccessful, it returns false.
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
