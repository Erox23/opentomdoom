# opentomdoom
OpentomDoom is my doom porting attempt for OpenTom that is working on TomTom One v3 device that I got for 1euro from local second hand.

It still has rendering issues that I will hopefully fix

To try it you will need:
- old TomTom device (tested on "TomTom One 3rd Edition(1GB)")
- libraries, crosscompiler and all the stuff needed to compile OpenTom for your device
- WAD file (game data). [better first try to compile it]
  
To compile you will need a working OpenTomSDK. If you are able to compile OpenTom and it's working on you device you will be able to compile and run Doom
1. Put files from /doomgeneric to /home/<user>/build/applications/src/ ("build" is where you did the OpenTom compilation)
2. I'm not sure if it's needed, but i do it =   sudo dpkg --add-architecture i386
3. Change AUTOROOT in "get_cross_env.sh" to your OpenTom dest (/home/<user>/build for example) and then -> source get_cross_env.sh
4. linux32 make
   And it should start to compile your OpenTomDoom ;)
### main loop (this line saved me)
At start, call doomgeneric_Create().

In a loop, call doomgeneric_Tick().

In simplest form:
```
int main(int argc, char **argv)
{
    doomgeneric_Create(argc, argv);

    while (1)
    {
        doomgeneric_Tick();
    }
    
    return 0;
}
```

## X11 - OpenTom
![Ubuntu](screenshots/tomtom.png)

