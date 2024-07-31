# Pegasus YouTube Report

`pegasus-youtube-report` adalah skrip Python untuk melaporkan video di YouTube menggunakan API dengan data yang diambil dari TikTok.

## Persyaratan

- Python 3.x
- Modul Python `requests`

## Instalasi

1. Clone repositori ini atau unduh sebagai ZIP.
2. Pastikan Python 3.x telah terinstal di sistem Anda.
3. Instal modul `requests` jika belum terinstal:
    ```bash
    pip install requests
    ```

## Penggunaan

1. Jalankan skrip `pegasus-youtube-report.py`:
    ```bash
    python pegasus-youtube-report.py
    ```
2. Masukkan `Video ID` dari TikTok ketika diminta.
3. Masukkan `YouTube Video Link` ketika diminta.
4. Skrip akan mengirim laporan ke YouTube dan menampilkan respons dari server.

## Kode Sumber

```python
import requests
import json

tiktok_video_id = input('Video ID > ')
youtube_video_link = input('YouTube Video Link > ')

url = "https://www.youtube.com/node/report/reasons_put?aid=1988&app_name=tiktok_web&device_platform=web_pc&device_id=6987530745909036549&region=DK&priority_region=&os=windows&referer=&root_referer=&cookie_enabled=true&screen_width=1920&screen_height=1080&browser_language=da-DK&browser_platform=Win32&browser_name=Mozilla&browser_version=5.0+(Windows+NT+10.0%3B+Win64%3B+x64)+AppleWebKit%2F537.36+(KHTML,+like+Gecko)+Chrome%2F92.0.4515.107+Safari%2F537.36&browser_online=true&verifyFp=verify_krfa96cw_p2Eae0I8_dJaE_4XwS_AEGm_KOmG1m49cOwX&app_language=en&timezone_name=Europe%2FCopenhagen&is_page_visible=true&focus_state=true&is_fullscreen=false&history_len=4&battery_info=1"

payload = json.dumps({
    "reason": 1004,
    "object_id": tiktok_video_id,
    "owner_id": "6636714219386781701",
    "report_type": "video"
})
headers = {
    'authority': 'www.youtube.com',
    'sec-ch-ua': '"Chromium";v="92", " Not A;Brand";v="99", "Google Chrome";v="92"',
    'accept': 'application/json, text/plain, */*',
    'x-secsdk-csrf-token': '000100000001ddd4e9748bc018f9e9c13093fb09bb878e0c97573abfdbf43ec8d0817c782b7a1694901c1b038c13',
    'sec-ch-ua-mobile': '?0',
    'tt-csrf-token': 'ePCjBjwO15QhaDbSrq7NMj6L',
    'user-agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/92.0.4515.107 Safari/537.36',
    'content-type': 'application/json',
    'origin': 'https://www.tiktok.com',
    'sec-fetch-site': 'same-origin',
    'sec-fetch-mode': 'cors',
    'sec-fetch-dest': 'empty',
    'referer': youtube_video_link,
    'accept-language': 'da-DK,da;q=0.9,en-US;q=0.8,en;q=0.7',
    'cookie': 'tt_webid_v2=6987530745909036549; tt_webid=6987530745909036549; cookie-consent={"ga":true,"af":true,"fbp":true,"lip":true,"version":"v2"}; s_v_web_id=verify_krfa96cw_p2Eae0I8_dJaE_4XwS_AEGm_KOmG1m49cOwX; MONITOR_WEB_ID=6987530745909036549; tt_csrf_token=ePCjBjwO15QhaDbSrq7NMj6L; R6kq3TV7=AGIivtV6AQAAN-OR-sxIv18EYkOMaPvth3F_97xkhJ_OT_yI7nG6UayUCYRk|1|0|d52a182c37413d8803c7100633cc49d673b8b993; ttwid=1|0D_adjNZXWbKipMeZG_RUyaNe6bFDSttsAX927MCOZ8|1627083654|4310fd827053a66f1886a63bea5b6d42b8b11ab91b563ac183eff76b902f48c9; csrf_session_id=d3b7880ce8d34ce0821782de56fae639'
}

response = requests.post(url, headers=headers, data=payload)

print(response.text)
print('Pegasus YouTube Report Completed')
