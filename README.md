import asyncio
from bleak import BleakScanner

async def scan_bluetooth():
    print("\n--- جاري فحص المحيط بحثاً عن أجهزة بلوتوث... ---")
    print("ملاحظة: هذا الفحص يكتشف أجهزة BLE (Bluetooth Low Energy)\n")
    
    # بدء عملية المسح
    devices = await BleakScanner.discover()
    
    if not devices:
        print("لم يتم العثور على أجهزة بلوتوث قريبة.")
    else:
        print(f"{'العنوان (Address)':<20} | {'الاسم (Name)':<20} | {'قوة الإشارة (RSSI)'}")
        print("-" * 60)
        for d in devices:
            print(f"{d.address:<20} | {str(d.name):<20} | {d.rssi} dBm")

def main_menu():
    print("=============================")
    print("        برنامج Rakon          ")
    print("=============================")
    print("1. فحص البلوتوث (Bluetooth Scanner)")
    print("2. الخروج")
    print("=============================")

if __name__ == "__main__":
    while True:
        main_menu()
        choice = input("اختر رقماً: ")
        
        if choice == "1":
            asyncio.run(scan_bluetooth())
        elif choice == "2":
            print("إلى اللقاء!")
            break
        else:
            print("خيار غير صحيح، حاول مرة أخرى.")
