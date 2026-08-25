# mijn-pc-setup

Hoe mijn werkplek is opgebouwd. Als deze pc morgen stukgaat, bouw ik hem hiermee terug.

Laatst bijgewerkt: augustus 2026

## De machine

| Onderdeel | Wat |
| --- | --- |
| Processor | Intel Core i7-7700, 4 cores |
| Geheugen | 32 GB DDR4-2400 (4 x 8 GB Samsung, 4 van 4 sleuven bezet) |
| Schijven | C: SSD (systeem + code), D: HDD (opslag) |
| Grafisch | Intel HD 630 onboard, 2 videopoorten |
| Windows-gebruiker | Gebruiker |
| Linux-gebruiker (WSL2) | ruud |

## Wat er is ingesteld

### 1. Virtualisatie aan in de BIOS

Nodig voor WSL2. Zonder dit start Ubuntu niet.

### 2. WSL2 met Ubuntu

Geinstalleerd via `wsl --install`. Dit is de plek waar ik code draai.

### 3. Geheugenlimiet voor WSL2

Zonder limiet pakt WSL2 te veel en gaat Windows swappen naar schijf.
Het bestand staat op Windows in `C:\Users\Gebruiker\.wslconfig`:

```
[wsl2]
memory=12GB
processors=4
swap=4GB
```

Na wijzigen altijd `wsl --shutdown` draaien, anders blijft de oude limiet actief.
Controleren in Ubuntu met `free -h` - bij Mem total moet ongeveer 11Gi staan.

### 4. Defender-uitsluitingen

Windows Defender scant elk bestand dat node, git en python aanraken. Dat maakt installeren en builden traag.
Uitgesloten: mijn code-mappen, plus de programma's node, git, code (VS Code), npm en python.

Let op: dit is een bewuste afweging. Minder scannen is sneller, maar ook minder bescherming.
Alleen doen voor mappen waar ik zelf code in zet, nooit voor Downloads.

### 5. Windows opgeschoond

- Opstartapps uitgezet die ik niet nodig heb
- Visuele effecten en transparantie uit
- Achtergrond-apps beperkt
- Energiebeheer op hoge prestaties
- Schijfopruiming gedraaid, Storage Sense aan

### 6. Git

```
git config --global user.name "Ruud"
git config --global user.email "228929390+ruudbonne500-cmd@users.noreply.github.com"
git config --global init.defaultBranch main
```

Dat e-mailadres is het verbergadres van GitHub, zodat mijn echte adres niet in publieke commits staat.

### 7. SSH-sleutel

```
ssh-keygen -t ed25519 -f ~/.ssh/id_ed25519 -N "" -C "wsl2-desktop"
cat ~/.ssh/id_ed25519.pub
```

De publieke helft komt op github.com/settings/keys. De geheime helft blijft op deze pc en deel ik nooit.

## Volgorde bij een nieuwe pc

1. Windows installeren en bijwerken
2. Virtualisatie aanzetten in de BIOS
3. `wsl --install` draaien, pc herstarten
4. `.wslconfig` aanmaken met de instellingen hierboven
5. Defender-uitsluitingen instellen
6. VS Code installeren plus de WSL-extensie
7. Git instellen en een nieuwe SSH-sleutel maken
8. Windows opschonen (opstartapps, visuele effecten, energiebeheer)

## Wat ik heb geleerd

- Een pc die twaalf dagen aanstaat wordt traag. Gewoon herstarten helpt.
- Geheugen vol betekent swappen naar schijf, en dat voel je overal.
- 16 GB was te weinig naast WSL2. Met 32 GB is het probleem weg.
- Vier identieke reepjes is beter dan gemengde: geen snelheidsverlies.

## Nog te doen

- [ ] SSH-sleutel koppelen aan GitHub
- [ ] Tweede scherm aansluiten
- [ ] Back-upplan maken voor als de SSD stukgaat
