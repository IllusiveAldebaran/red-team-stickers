The files not in a subdirectory are less compressed to the rigid sticker rules.

Images can be `webp` or `png`. Animated ones are `apng`.

Sticker packs are immutable so there are separate versions here as `v1`, `v2`, etc.
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
# original is 10 seconds long (hence the 10) and I wanted it to be 3 seconds long (hence the 3) (3/10)
ffmpeg -i original_vid.gif -filter:v "setpts=(3/10)*PTS" vid2.apng

# Changing the framerate to 30fps (60fps is also fine I think)
ffmpeg -i vid2.apng -filter:v fps=30 vid3.apng

# Example of making an apng smaller
`ffmpeg -i explaining.apng -vf "fps=20,scale=160:-1:flags=lanczos,split[s0][s1];[s0]palettegen=max_colors=16:reserve_transparent=1[p];[s1][p]paletteuse" -s 160x160 -plays 0 animated/explaining.apng`
```
The `-s 160x160` makes it a square, `-plays 0` makes it loop correctly, `max_colors=16` creates indexes the animation by color. This is a major improvement on size.
