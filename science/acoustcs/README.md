# Acoustics Hearing

[![Python](https://img.shields.io/badge/python-3.9%2B-3776AB?logo=python&logoColor=white)](https://www.python.org/)
[![Coverage](https://img.shields.io/badge/coverage-87.31%25-brightgreen)](doc/coverage)
![scicov](https://img.shields.io/badge/scicov-10-ff69b4)

Biologisch inspiriertes Modell fuer auditive Raumorientierung, feline
Hoerphysiologie, Cochlea-Filterung und digitale A/D-Wandlung. Die
Implementierung begleitet die wissenschaftliche Arbeit
`science/acoustcs/science/acoustcs.tex` und bildet insbesondere die Inhalte
aus den Kapiteln 8, 9 und 10 numerisch ab.

## Inhalt der Arbeit

### Kapitel 8: Auditive Raumorientierung

Das Modell beschreibt Schall als zeitlich praezises Orientierungsmedium und
quantifiziert die wichtigsten binauralen Hinweisreize:

- Interaurale Zeitdifferenz (ITD) nach dem Woodworth-Schlosberg-Modell
- Interauraler Pegelunterschied (ILD) mit Frequenzabhaengigkeit
- Just Noticeable Difference (JND) fuer ITD
- Fisher-Information und Cramer-Rao-Schranke fuer die
	Lokalisierungsgenauigkeit
- raumbezogene Shannon-Entropie bei Hoerverlust
- bilaterale Asymmetrie und Front-Back-Verwechslung

Die verwendete Schallgeschwindigkeit betraegt standardmaessig `343 m/s`.

$$
\mathrm{ITD}(\theta) = \frac{r_{\mathrm{head}}}{c}\sin(\theta).
$$

### Kapitel 9: Felines Gehoer

`FelineAuditory` stellt physiologische Parameter fuer Katze, Hund und Mensch
bereit und berechnet daraus vergleichbare Kennwerte:

- Hoerbereiche: Katze `55 Hz` bis `77 kHz`, Hund `100 Hz` bis `45 kHz`,
	Mensch `20 Hz` bis `20 kHz`
- Frequenzbandbreite und Oktavumfang
- cochleaere Laenge und Greenwood-Skalierung
- kritische Bandbreite und Q-Faktor
- cochleaere Verstaerkung
- Refraktaerperiode, Phasenlocking und zeitliche Aufloesung
- ITD-Maximum und Lokalisierungsgenauigkeit mit fixiertem oder beweglichem Ohr
- Shannon-Kapazitaet und vergleichender Ueberlegenheitsindex

Die Tonotopie bildet Frequenz logarithmisch auf die Position entlang der
Cochlea ab: hohe Frequenzen liegen basal, niedrige Frequenzen apikal.

### Kapitel 10: Cochlea-Modell und A/D-Wandlung

Die Cochlea wird als ortsabhaengiges mechanisches System modelliert. Die
Basilarmembran verwendet ortsabhaengige Masse, Steifigkeit und Daempfung:

$$
m(x)\,w_{tt} + c(x)\,w_t + k(x)\,w
= p_{\mathrm{in}}(x,t) - p_{\mathrm{out}}(x,t).
$$

Enthalten sind:

- Greenwood-Tonotopie und inverse Positionsabbildung
- mechanische Impedanz und Admittanz
- Resonanzfrequenzen und Qualitaetsfaktor
- OHC-Verstaerkung und IHC-Sigmoidantwort
- Gammatone-nahe Butterworth-Bandpassfilter
- logarithmisch angeordnete Cochlea-Filterbank
- Cochleagramm als logarithmische Zeit-Frequenz-Darstellung
- Sample-and-Hold und Quantisierung
- Quantisierungsfehler und SNR
- optionale Sigma-Delta-Modulation mit Dezimationsfilter

Die Standardimplementierung verwendet `96 kHz`, `24 Bit` und `128`
Filterkanaele. Die Filterbank liefert ein Array der Form
`(Kanaele, Samples)`.

## Projektstruktur

```text
src/acoustcs/
	audio_converter.py       A/D-Wandlung und Quantisierung
	cochlear_model.py        Basilarmembran und Cochlea-Mechanik
	feline_auditory.py       Katzen-, Hunde- und Menschenmodell
	filterbank.py            Gammatone-nahe Cochlea-Filterbank
	spatial_localization.py  ITD, ILD und Raumlokalisierung
tests/                       Automatisierte Tests
science/acoustcs.tex         Wissenschaftliche Arbeit
```

## Installation

PowerShell im Projektverzeichnis:

```powershell
cd C:\Users\sepp5.AD\Git\science\science\acoustcs
.\venv\Scripts\Activate.ps1
python -m pip install ".[dev]"
```

Ohne Aktivierung der virtuellen Umgebung:

```powershell
.\venv\Scripts\python.exe -m pip install ".[dev]"
```

## Tests ausfuehren

```powershell
.\venv\Scripts\python.exe -m pytest
```

Coverage-Berichte werden entsprechend der `pyproject.toml` unter
`doc/coverage` erzeugt.

## Kurzes Beispiel

```python
import numpy as np

from acoustcs import FelineAuditory, SpatialLocalization
from acoustcs.audio_converter import AudioConverter
from acoustcs.filterbank import CochlearFilterBank

cat = FelineAuditory()
print(cat.summary())

localization = SpatialLocalization()
itd = localization.itd_woodworth_schlosberg(30.0)
print(f"ITD: {itd * 1e6:.2f} us")

filterbank = CochlearFilterBank(n_channels=32)
signal = np.zeros(9600)
cochleagram = filterbank.apply_filterbank(signal)
print(cochleagram.shape)

converter = AudioConverter(bit_depth=24)
samples = converter.quantize(signal)
print(f"Quantisierungs-SNR: {converter.quantization_snr():.2f} dB")
```

## Wissenschaftlicher Kontext

Die Kapitel 8 bis 10 verbinden psychoakustische Raumhinweise, vergleichende
Hoerphysiologie und ein mechanisch motiviertes Cochlea-Modell. Das Python-
Paket ist als reproduzierbare numerische Begleitung gedacht: Die Formeln aus
der Arbeit werden parametrisiert, simuliert und durch Tests auf Randfaelle,
Monotonie, Skalierung und Integration geprueft.

## Erwerb

Der Preis für diese Arbeit und Software beträgt 521.000.000,00 EUR.

### Zahlungsinformationen

Name: Stephan Epp  
IBAN: DE24 5003 1900 0012 5603 20
BIC: BBVADEFFXXX