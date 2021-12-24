# Geekworm-X735-V2.5-Software
Installare il software per il Geekworm X735 V2.5 su Raspberry Pi OS

## Procedura per Debian Buster/Debian 10
URL originale: [Wiki Geekworm](https://wiki.geekworm.com/X735_V2.5_Software)

Repository GitHub: [geekworm-com](https://github.com/geekworm-com/x735-v2.5)

> **Nota Bene**: Come riportato dalla pagina wiki, ***"This guide is only for X735 V2.5 shield based on RASPBIAN. (Not tested on Ubuntu, openmediavault, retropie or other third party OS like Manjaro,RoninDojo.) "***

### Installazione
Assumendo che il sistema è aggiornato, aggiungere i seguenti pacchetti:
```bash
sudo apt-get install -y python-smbus python
sudo apt-get install -y pigpio python-pigpio python3-pigpio git
git clone https://github.com/geekworm-com/x735-v2.5
cd x735-v2.5
sudo chmod +x *.sh
sudo bash install.sh
echo "alias x735off='sudo x735softsd.sh'" >> ~/.bashrc
sudo reboot
```

### Test funzionamento "spegnimento sicuro"
```bash
x735off
```
- premere il pulsante per 1-2 secondi per riavviare
- premere il pulsante per 3 secondi per lo "spegnimento sicuro"
- premere il pulssante per 7-8 secondi per forzare lo spegnimento

### Disinstallazione

```bash
cd $HOME/x735-v2.5
sudo ./uninstall.sh
```

### Lettura della velocitá della ventola
```bash
echo "python3 /home/pi/x735-v2.5/pwm_fan_control.py &" >> $HOME/.bashrc
```
Questo comando aggiunge una riga in fondo al file ```.bashrc```. In questo modo, lo script python che gestisce la velocitá della ventola sará eseguito quando l'utente accederá al sistema.

Dopo un riavvio, è possibile ottenere informazioni sulla velocitá della ventola lanciando il comando
```bash
python3 $HOME/x735-v2.5/read_fan_speed.py
```
