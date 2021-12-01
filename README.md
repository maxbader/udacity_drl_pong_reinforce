# udacity_drl_pong_reinforce

## Issues
Using the original Udacity code gave me the following issues.

### Exception: ROM is missing for pong
```python
Exception: ROM is missing for pong, see https://github.com/openai/atari-py#roms for instructions
```
This problem was solved by adding 
```python
from pathlib import Path
if not Path('rars').is_dir():
    import urllib.request
    urllib.request.urlretrieve('http://www.atarimania.com/roms/Roms.rar','Roms.rar')
    !pip install unrar
    !unrar x Roms.rar
    !mkdir rars
    !mv HC\ ROMS.zip   rars
    !mv ROMS.zip  rars
    !python -m atari_py.import_roms rars
```

### Exception: AttributeError: 'HTMLWriter'
```python
AttributeError: 'HTMLWriter' object has no attribute '_temp_names' 
```
Thanks to https://teratail.com/questions/280493

This problem was solved by adding the follong block in pong_utils.py before `def animate_frames(frames):`

```python
from IPython.display import HTML
def display_animation(anim):
    plt.close(anim._fig)
    return HTML(anim.to_jshtml())
```
And replacing `display(display_animation(fanim, default_mode='once'))` with `display(display_animation(fanim))`
