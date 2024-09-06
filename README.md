# Google Fonts API for developer - @T7C

# Google Fonts

1. Cách sử dụng:
```bash
pip install requests
```
2. **Sử dụng mã dưới đây để lấy toàn bộ danh sách các fonts và file tff:**
```python
import requests


api_key = 'AIzaSyDR1wPN6S4-l-1fSstrl13m87K7zffi630' # api gg fonts hoàn toàn miễn phí
url = f'https://www.googleapis.com/webfonts/v1/webfonts?key={api_key}&sort=popularity'


response = requests.get(url)


if response.status_code == 200:
    data = response.json()
    
 
    for font in data['items']:
        family = font['family']
        variants = font.get('variants', [])
        files = font.get('files', {})
        
        print(f"Font Family: {family}")
        print("Variants and Links:")
        

        for variant in variants:
            link = files.get(variant)
            if link:
                print(f"  {variant}: {link}")
            else:
                print(f"  {variant}: No TTF file available")
        
        print("-----")
else:
    print(f"Error: {response.status_code}")

```

Ảnh sau khi chạy: 
![example](images/image.png)



3. **Lấy danh sách phông chữ**
 ```python
    import requests

    api_key = 'AIzaSyDR1wPN6S4-l-1fSstrl13m87K7zffi630'
    url = f'https://www.googleapis.com/webfonts/v1/webfonts?key={api_key}&sort=popularity'

    response = requests.get(url)

    if response.status_code == 200:
        data = response.json()
        for font in data['items']:
            print(f"Font Family: {font['family']}")
    else:
        print(f"Error: {response.status_code}")
 ```


4. **lấy danh sách font trong css**
```python
import requests


api_key = 'AIzaSyDR1wPN6S4-l-1fSstrl13m87K7zffi630'
url = f'https://www.googleapis.com/webfonts/v1/webfonts?key={api_key}&sort=popularity'


response = requests.get(url)

if response.status_code == 200:
    data = response.json()
 
    for font in data['items']:
        family = font['family']
        variants = font.get('variants', [])
        
      
        weights = [str(v) for v in variants if v.isdigit()]
        if not weights:
            weights = ['400']  

        weights_str = ';'.join(weights)
        
        
        css_link = f'https://fonts.googleapis.com/css2?family={family.replace(" ", "+")}:wght@{weights_str}&display=swap'
        
        print(f"Font Family: {family}")
        print(f"CSS Link: {css_link}")
        print("-----")
else:
    print(f"Error: {response.status_code}")

```

 cách chèn vào HTML: 
 <style>
    @import url ('https://fonts.googleapis.com/css?family=Roboto&display=swap');
    </style>


## tài liệu tham khảo

[Google Fonts for developer](https://developers.google.com/fonts/docs/getting_started?hl=vi)
[Google Fonts API](https://developers.google.com/fonts/docs/developer_api?hl=vi)