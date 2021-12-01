# udacity_drl_pong_reinforce


## Issus
Using the origianl udacity code gave me the follwoing error
### Exception: ROM is missing for pong
```
Exception: ROM is missing for pong, see https://github.com/openai/atari-py#roms for instructions
```
This problem was solved by adding 
```
import urllib.request
urllib.request.urlretrieve('http://www.atarimania.com/roms/Roms.rar','Roms.rar')
!pip install unrar
!unrar x Roms.rar
!mkdir rars
!mv HC\ ROMS.zip   rars
!mv ROMS.zip  rars
```
### Exception: AttributeError: 'HTMLWriter'
```
AttributeError: 'HTMLWriter' object has no attribute '_temp_names' 
```
Thanks to https://teratail.com/questions/280493

This problem was solved by adding the follong block in pong_utils.py before `def animate_frames(frames):`

```
from IPython.display import HTML
def display_animation(anim):
    plt.close(anim._fig)
    return HTML(anim.to_jshtml())
```
And replacing `display(display_animation(fanim, default_mode='once'))` with `display(display_animation(fanim))`
