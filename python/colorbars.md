# Custom Themed Colorbar in Matplotlib

Custom, Disney Princess themed colorbars for Matplotlib visualizations.

Color inspired from [https://leahsmyth.github.io/Princess-Colour-Schemes/index.html](https://leahsmyth.github.io/Princess-Colour-Schemes/index.html).


## Prerequisites
```python
from matplotlib.colors import LinearSegmentedColormap
def create_custom_colormap(base_colors): return LinearSegmentedColormap.from_list('custom_cmap', base_colors)
```


## Colorbars

### 🐚 Ariel
```python
ArielGreenCMAPBaseColor = ['#ffffff', '#c6e8be', '#53b288', '#378d68']
ArielGreenCMAP = create_custom_colormap(ArielGreenCMAPBaseColor)
```

```python
ArielPurpleCMAPBaseColor = ['#ffc4f6', '#a497c4', '#594597']
ArielPurpleCMAP = create_custom_colormap(ArielPurpleCMAPBaseColor)
```

```python
CinderellaCMAPBaseColor = ['#ffffff', '#d7eaf6','#b1def5','#8cc5e8','#3b8bbd','#286287']
CinderellaCMAP = create_custom_colormap(CinderellaCMAPBaseColor)
```

### 📕 Belle
```python
BelleCMAPBaseColor = ['#ffffff', '#ffefb5','#f7e4a6','#ffe67f','#f8d562','#f0be4d','#e3b348',]
BelleCMAP = create_custom_colormap(BelleCMAPBaseColor)
```

### 💤 Aurora
```python
AuroraPinkCMAPBaseColor = ['#ffffff', '#e5afcf', '#e387b8', '#d2487a']
AuroraPinkCMAP = create_custom_colormap(AuroraPinkCMAPBaseColor)
```

### ☀️ Rapunzel
```python
RapunzelCMAPBaseColor = ['#ffffff', '#fadee4', '#daafd2', '#9c8cbd', '#a06baf', '#8550a0']
RapunzelCMAP = create_custom_colormap(RapunzelCMAPBaseColor)
```

### 🍃 Pocahontas
```python
PocahontasCMAPBaseColor = ['#ffffff', '#f9e0ab', '#f7cb6c', '#da9740', '#c74e28']
PocahontasCMAP = create_custom_colormap(PocahontasCMAPBaseColor)
```

### 🌻 Anna
```python
AnnaCMAPBaseColor = ['#a42384', '#1d318b', '#040a0a']
AnnaCMAP = create_custom_colormap(AnnaCMAPBaseColor)
```

### ❄️ Elsa
```python
ElsaCMAPBaseColor = ['#d5d9ea', '#82d4ed', '#3abae3', '#0c77a8']
ElsaCMAP = create_custom_colormap(ElsaCMAPBaseColor)
```
