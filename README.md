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

## Procedura per Python3 + Debian Bullseye/Debian 11
Repository GitHub: [thorkseng](https://github.com/thorkseng/x735-v2.5)

### Installazione
Questi script sono stati testati su Raspberry Pi OS Bullseye. Sono stati aggiornati, rispetto agli script originali, per poter utilizzare Python3
```bash
sudo apt install python3 python3-smbus python3-pigpio
sudo apt install pigpio
sudo apt install git
git clone https://github.com/thorkseng/x735-v2.5/
cd x735-v2.5
sudo chmod +x *.sh
sudo bash install.sh
sudo reboot
```

### Installazione del servizio
Lo script shell ```install_service.sh```
1. crea un nuovo servizio nella cartella ```/etc/systemd/system/``` con il nome ```x735fan.service```
2. Lo abilita, lo attiva e controlla che sia in esecuzione.
   In tal caso, l'esecuzione dello script python sará rimosso dal file ```.bashrc```
   
Basterá eseguire lo script:
```bash
sudo bash $HOME/x735-v2.5/install_service.sh
```

### Utilizzo
Per attivare manualmente la ventola, eseguire il comando seguente:
```bash
python3 $HOME/x735-v2.5/pwm_fan_control.py
```
Il comando viene aggiunto, in background, anche nel file ```.bashrc``` del profilo dell'utente.

Per leggere la velocitá della ventola, eseguire il comando
```bash
python3 $HOME/x735-v2.5/read_fan_speed.py
```
