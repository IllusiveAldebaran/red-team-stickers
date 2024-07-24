Images can be `webp` or `png`. Animated ones are `apng`.
Sticker packs are immutable so there are separate versions here as `v1`, `v2`, etc.
For this reason it's probably best to wait before creating a pack. 

For now, add your images and videos to `v2/{animated/,static/}`

Each has `animated/` and `static/`, but that's honestly by choice.

[v1 pack download](https://signal.art/addstickers/#pack_id=75a162e4696c935f0ba07e21c9358409&pack_key=28aa7683725439ab0a86d53cff1d3a088e9bfda6cef4326273372c0f4aee38aa)
# Links
### Guides-Info
Read the blog post first:
[Signal Blog Post on Stickers](https://support.signal.org/hc/en-us/articles/360031836512-Stickers)
[signalstickers](unofficial library for download)
[Comprehensive Reddit Guide](https://www.reddit.com/r/signal/comments/kxa631/a_comprehensive_guide_to_find_and_create_stickers/)

### For Creation Resources
[If you're lazy to create a pack](https://ezgif.com/)
[Scripts](https://github.com/signalstickers/stickers-scripts)

Unlike images, animations aren't really tweaked before trying to add them as sticker, so they take some preparation.
Some useful examples of commands for a suitable sticker used by Paco:
*I wrote this down a while ago, so I might be wrong I'm just copy pasting*


```
# The original gif is too long and need to shorten
# original is 10 seconds long instead of 3 seconds long (hence the 3/10)
ffmpeg -i original_vid.gif -filter:v "setpts=(3/10)*PTS" vid2.apng

# Changing the framerate to 30fps (60fps is also fine I think)
ffmpeg -i vid2.apng -filter:v fps=30 vid3.apng

# Example of cropping to a square 240x240 because original is too tall
# If no x,y coordinates are specified then the crop is centered
ffmpeg -i goku-prowler-goku.apng -vf "crop=240:240:0:300" goku-prowler.apng

# Instead of cropping a 300x400 adding transparenty padding to make 400x400 square
# Hence the color=0x00000000
ffmpeg -i goku-vegeta.apng -vf "scale=400:400:force_original_aspect_ratio=decrease,pad=400:400:(ow-iw)/2:(oh-ih)/2:color=0x00000000,setsar=1" goku-vegeta-wide.apng

# Example of making an apng smaller and size is squeezed into 160x160, both by the scale=160 option and -s 160x160
`ffmpeg -i explaining.apng -vf "fps=20,scale=160:-1:flags=lanczos,split[s0][s1];[s0]palettegen=max_colors=16:reserve_transparent=1[p];[s1][p]paletteuse" -s 160x160 -plays 0 animated/explaining.apng`
```
The `-s 160x160` makes it a square, `-plays 0` makes it loop correctly, `max_colors=16` creates indexes the animation by color. This is a major improvement on size.

If stickers bitches about size, make it a square with `-s NUMxNUM`
If it's about needing to loop, `-plays 0`
If it's too big, `max_colors=NUM` is a major improvement by having it, but it's probably the size. 340x340 is usually a good compromise on 2 second `apng`s.
