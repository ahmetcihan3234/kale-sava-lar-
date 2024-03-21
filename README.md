import random

class Kale:
    def __init__(self, isim, sahip):
        self.isim = isim
        self.sahip = sahip
        self.can = 100
        self.savunma_gucu = 50
    
    def saldir(self, rakip_kale):
        saldiri_gucu = random.randint(1, 20)
        hasar = saldiri_gucu - rakip_kale.savunma_gucu
        if hasar > 0:
            rakip_kale.can -= hasar
            print(f"{self.isim} tarafından {rakip_kale.isim} kaleye saldırıldı! Hasar: {hasar}")
        else:
            print(f"{self.isim} tarafından {rakip_kale.isim} kaleye saldırı başarısız oldu!")

class Oyuncu:
    def __init__(self, isim, saldiri_gucu, savunma_gucu):
        self.isim = isim
        self.saldiri_gucu = saldiri_gucu
        self.savunma_gucu = savunma_gucu
        self.can = 100

    def saldir(self, rakip):
        saldiri_gucu = random.randint(1, self.saldiri_gucu)
        savunma_gucu = random.randint(1, rakip.savunma_gucu)
        hasar = saldiri_gucu - savunma_gucu
        if hasar > 0:
            rakip.can -= hasar
            print(f"{self.isim} tarafından {rakip.isim}'e saldırıldı! Hasar: {hasar}")
        else:
            print(f"{self.isim} tarafından {rakip.isim}'e saldırı başarısız oldu!")

# 13 oyuncunun savaşını simüle eden kod
oyuncular = []
for i in range(1, 14):
    oyuncu = Oyuncu(f"Oyuncu {i}", random.randint(10, 25), random.randint(10, 25))
    oyuncular.append(oyuncu)

while any(oyuncu.can > 0 for oyuncu in oyuncular):
    oyuncu1, oyuncu2 = random.sample(oyuncular, 2)
    oyuncu1.saldir(oyuncu2)
    oyuncu2.saldir(oyuncu1)
    print(", ".join([f"{oyuncu.isim} Can: {oyuncu.can}" for oyuncu in oyuncular]))

hayatta_kalanlar = [oyuncu for oyuncu in oyuncular if oyuncu.can > 0]
if len(hayatta_kalanlar) == 1:
    print(f"{hayatta_kalanlar[0].isim} kazandı!")
else:
    print("Berabere!")

# Kale savunma oyununun eşleştirme kodu
import random

oyuncular = ["Oyuncu {}".format(i) for i in range(1, 14)]

def eslestirme_olustur(oyuncular):
    random.shuffle(oyuncular)
    eslestirmeler = []
    while len(oyuncular) >= 2:
        if len(oyuncular) >= 3:
            grup = oyuncular[:3]
            oyuncular = oyuncular[3:]
        else:
            grup = oyuncular[:2]
            oyuncular = oyuncular[2:]
        eslestirmeler.append(grup)
    return eslestirmeler

eslestirmeler = eslestirme_olustur(oyuncular)
for i, eslestirme in enumerate(eslestirmeler, start=1):
    print("Eşleştirme {}: {}".format(i, ", ".join(eslestirme)))

# Kale savunma oyununun ana kodu
kaleler = []
for i in range(1, 14):
    kale = Kale(f"Kale {i}", f"Oyuncu {i}")
    kaleler.append(kale)

while any(kale.can > 0 for kale in kaleler):
    saldiran_kale = random.choice(kaleler)
    hedef_kaleler = [k for k in kaleler if k != saldiran_kale]
    hedef_kale = random.choice(hedef_kaleler)
    saldiran_kale.saldir(hedef_kale)
    print(", ".join([f"{kale.isim} Can: {kale.can}" for kale in kaleler]))

kazanan_kaleler = [kale for kale in kaleler if kale.can > 0]
if len(kazanan_kaleler) == 1:
    print(f"{kazanan_kaleler[0].isim} kazandı!")
else:
    print("Berabere!")
