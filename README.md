# Clash Config Generator
Script ini untuk membuat config clash dengan template yang sama dengan daftar di atas. 
memiliki 3 output:
1. Config All dalam satu file
   - kita cuma masukin akun v2ray dan otomatis jadi config dengan fitur addblock dan family safe
2. output proxies only dan generate proxy providers
3. output config dan proxy provider terpisah
next__ coming soon!


Script: `clashmi.py`


Cara Penggunaan di Termux:

1. Install Dependencies:

```bash
pkg update && pkg upgrade
pkg install python python-pip
pip install pyyaml
```

2. Simpan Script:

```bash
nano clash_generator.py
# Paste script yang ada di clashmi.py, lalu save (Ctrl+X, Y, Enter)
```

3. Berikan Permission:

```bash
chmod +x clash_generator.py
```

4. Jalankan Script:

```bash
python clash_generator.py
```

Fitur yang Didukung:

Protocol	| Support |	Keterangan	
:--- | :--- | :---
VMess |	✅	| WS, gRPC, TLS	
VLESS	| ✅ |	Reality, XTLS, WS, gRPC	
Trojan	| ✅ |	WS, gRPC, TLS	
Shadowsocks |	✅ |	SIP002, Plugin Obfs	
ShadowsocksR	| ✅ |	Semua method	
Hysteria	| ✅	| Hysteria 1 & 2	
TUIC | 	✅ |	v5	
WireGuard |	✅	| WG URL format	
SOCKS5 |	✅	| Dengan auth	
HTTP	| ✅	| Dengan TLS	


Fitur:

1. Mode Input 

```
  				1. Single 
  				2. Multi-input
  				3. Clipboard
```

2. Proxy Group MANUAL (Full Config Mode)
Saat memilih Mode A (Full Config), proxies otomatis masuk ke group `MANUAL`:

```yaml
proxy-groups:
  - name: MANUAL
    type: select
    proxies:
      - BEST-PING
      - FALLBACK
      - LB
      - VMess-143022      # ← Proxy 1
      - VLESS-143023      # ← Proxy 2
      - Trojan-143024     # ← Proxy 3
      # ... semua proxy lainnya
    
  - name: FALLBACK
    type: fallback
    proxies:
      - VMess-143022      # ← Semua proxy juga masuk sini
      - VLESS-143023
      - Trojan-143024
    
  - name: BEST-PING
    type: url-test
    proxies:
      - VMess-143022      # ← Semua proxy juga masuk sini
      - VLESS-143023
      - Trojan-143024
```

3. Flow Full Config Mode:
1. Hapus `proxy-providers`
2. Hapus `use:` dari semua groups
3. Masukkan semua proxy names ke:
   - `MANUAL` (setelah BEST-PING, FALLBACK, LB)
   - `FALLBACK`, `BEST-PING`, `LB` (untuk health-check)
4. Tambah section `proxies:` di akhir config

Cara Pakai:

```bash
python clash_generator.py

# Pilih mode:
# 1 = Single URL
# 2 = Multi-input (banyak URL)
# 3 = Clipboard

# Pilih output:
# a = Full config (proxies masuk ke MANUAL group)
# b = Proxy provider mode
# c = Proxies only
```
