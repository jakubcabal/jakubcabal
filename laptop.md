# Framework Laptop 13

- System: Ryzen™ AI 5 340
- Display: 2.8K Display
- Memory: DDR5-5600 - 32GB (2 x 16GB)
- Storage: WD_BLACK™ SN7100 NVMe™ - M.2 2280 - 500GB
- Expansion Cards: 2x USB-C (Aluminum), 1x USB-A, 1x HDMI (3rd Gen)

## Vylepšováky

FrameWork Laptop 13 funguje s Fedorou 42 velmi dobře, ale pár drobností jsem ještě více vylepšil...

### Automatické odemikání šifrovaného oddílu pomocí TMP2

```
sudo systemd-cryptenroll --wipe-slot tpm2 --tpm2-device auto --tpm2-pcrs "1+3+5+7+11+12+14+15" /dev/nvme0n1p3
sudo dracut -f
```

Viz návod zde: https://community.frame.work/t/guide-setup-tpm2-autodecrypt/39005

### Digitalní mikrofon

Digitalní mikrofon pod Linuxem podle všeho vůbec nefunguje a je potřeba používat analogovou verzi.
Pro méně komplikovaný život je nejlepší rovnou zakázat jeho ovladač.
Vytvořte soubor `/etc/modprobe.d/blacklist-snd_soc_dmic.conf` s následujícím obsahem:
```
blacklist snd_soc_dmic
blacklist snd_acp_legacy_mach
blacklist snd_acp_mac
```

Zdroj: https://community.frame.work/t/laptop13-ryzen-ai-340-internal-mic-in-fedora42-doesnt-work/75748/11

### Občasné problikávání obrazovky ve Firefoxu

Objevil jsem [grafický bug s problikávající obrazovkou](https://youtu.be/TDF-SJ1IqJ0?si=aSxtN-LvwKktYuYX), který se projevuje při pohybu kurozoru na některých webech (například: ) ve Firefoxu.
Problém lze  vyřešit vložením `MUTTER_DEBUG_DISABLE_HW_CURSORS=1` do souboru `/etc/environment` a restartováním.

Zdroj: https://community.frame.work/t/flickering-when-using-firefox-under-kde-wayland-on-ryzen-ai-300/69599/51
