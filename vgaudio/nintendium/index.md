## Nintendium Philharmonic: The History of the Sound of Nintendo Gaming Consoles From the Famicom to the Wii

*(Note: While the content of this paper has been left more or less unmodified, we've made some significant changes for readability in a website format. Trust us, you're better off reading it like this.)*

### Introduction

Though too often underappreciated, sound design is one of the most crucial features of making a successful game. Good music and sound effects can accentuate the best features and desired aesthetic of a game’s visuals and mechanics. Whether the joyous romps of *Super Mario Bros.*, the mysterious dungeon hymns of *The Legend of Zelda*, or the sparse, environmental melodies of *Metroid*, Nintendo’s iconic games would not be the same without their music.

However, the power imbued in good sound design comes with a large cost, particularly for retro consoles. The extremely simple, robust sound chips featured on old consoles required extremely specific expertise to make sound, let alone enjoyable music, due to their highly limited, low-resolution simple wave or wavetable-based sound generation. Video game composers before the era of CD-quality audio straddled the line between composer, sound designer, and programmer.

In this paper I will discuss the audio capabilities, software, and hardware of every Nintendo console, spanning from the Nintendo Entertainment System to the Nintendo Wii. For each console, I will discuss specific details of how the console produces audio, relevant general console information including release date and typical storage memory, important musical, audiological, or cultural features, and comparative details of consoles across brands or generations. To facilitate direct comparison between consoles, I will present an audio example from an entry in the Super Mario franchise on each console, and I will supplement information with additional examples from other games and series where necessary.

### The Nintendo Entertainment System

The Nintendo Entertainment System was released in 1983. Nintendo’s first gaming console, it is an 8-bit system with 5 completely analog audio channels with 4-bit quantization. Since the analog waveforms that the NES can produce can be sounded at any frequency, the console does not have a distinct sample rate. The Ricoh 2A03, an 8-bit microprocessor, is in charge of the NES’ audio processing. The NES APU is thoroughly documented on the NES DEV Wiki “APU” page[^nesdevwiki].

Four of the five channels on the RP2A03 can produce exactly one kind of analog waveform. The first two channels on the NES produce pulse waves. Each channel can produce a pulse wave with one of four different duty cycles. Additionally, both pulse waves can be modulated with a 4-bit constant or saw-shaped decay volume envelope as well as with a built-in linear pitch sweep. Channel three can produce a 4-bit quantized triangle wave. This channel does not have volume envelope or pitch sweep functionality, and is therefore essentially limited to being on or off at a given pitch. The fourth channel is a noise generator with the same volume envelopes as the pulse channels. Noise can be used to emulate the sounds of percussion and impacts. The noise channel uses a 15-bit linear-feedback shift register to generate a pseudorandom sequence of 1-bit numbers at a given rate by starting with a value of 000000000000001, shifting each bit down a place every step, and placing the bitwise exclusive-or (that is, 1 if the two values are different, 0 if they are the same) of two bits in the most significant bit on each step.

> To better understand the LFSR, I wrote an emulation of it in C: [proto.ml/lfsr](/lfsr)

This generator has two modes: In mode 0, the XOR of bits 0 and 1 is used, created a 32,767 step sequence that sounds like white noise; in mode 1, the XOR of bits 0 and 6 is used, creating a 31 or 93 step sequence with the distinct tone of a metallic “clank.” In a typical NES music composition, these four channels are used for the melody, harmony, bass, and percussion respectively.

<audio
    controls
	src="Megaman.mp3">
	Your computer does not support HTML in-line audio.
</audio>

> *Fire Man's theme from Mega Man (1987) excellently demonstrates both modes of the noise generator. Listen to the alternating metal clank and snare drum in the percussion. [Listen on YouTube](https://youtu.be/CTIdRD5qrag)*

The fifth NES sound channel allows for playback of custom waveforms. Often referred to as the delta modulation channel, it uses 1-bit delta pulse code modulation to efficiently store 7-bit PCM waveform data for playback at a variable rate. However, as most NES games were stored in 200kB cartridges, with even the largest games only taking up only 1MB, space for even DPCM waves was often too much to ask. Thus, this channel is by far the least used in NES games. While this channel could be used to supplement the four prescribed-wave channels with additional simple waveforms, the most memorable DMC sounds pushed the console to its absolute limit. With enough free space, the DMC channel could even play recorded voice clips! Even if these DMC recordings are not even decent quality by today’s standards, they are truly remarkable for their time and place.

<audio
    controls
	src="The Adventures of Bayou Billy.mp3">
	Your computer does not support HTML in-line audio.
</audio>

> *An often-cited example of the DMC's capabilities is a voice clip in The Adventures of Bayou Billy. [Listen on YouTube](https://youtu.be/cpd87e2PJnE?t=34)*

However, even five channels and custom waveforms wasn’t enough for the incredibly ambitious Nintendo of 1983. While this capability was not included in US-released NESes, Japanese Famicoms are capable of sending and receiving data from expansion chips in game cartridges. In addition to providing additional processing power, tools, or memory management capabilities, these expansion chips could open up additional sound channels on the Famicom. Some notable expansion chips are the Sunsoft 5B, which added additional square and noise waves to the sound of Mr. Gimmick!, Famicom Disc System (A Famicom add-on that allowed the loading of games from floppy discs) Audio, which offered the potential to employ wavetable synthesis, and the Konami VRC line of chips. Expansion chip composers often had to recompose game soundtracks for US release due to the lack of expanded sound channels. This difference can be heard in titles like Konami’s Castlevania III: Dracula’s Curse, for which the music was composed with the capabilities of the VRC6, with two extra pulse waves and a sawtooth wave, in mind.

<audio
	controls
	src="Akumajou Densetsu.mp3">
	Your computer does not support HTML in-line audio.
</audio>

<audio
	controls
	src="Castlevania III Dracula's Curse.mp3">
	Your computer does not support HTML in-line audio.
</audio>

> *Stage 1 from Akumajou Densetsu (JP) and Castlevania III: Dracula's Curse (US). The music was recomposed for the US version without expanded sound. [Listen on YouTube](https://youtu.be/Rh-vkpjyMTw)*
	
The player two controller on only the original Famicom (the Japanese name for the NES) with directly wired, non-removable controllers had a small-diaphragm condenser microphone instead of start and select buttons[^greathierophant]. This microphone is only capable of simple amplitude recognition, so a small assortment of games including Japanese versions of *The Legend of Zelda* and *Raid on Bungeling Bay* encourage the players to blow into the mic to destroy enemies, interact with NPCs, or trigger events. 

The Super Mario franchise piece I’ve chosen to represent the NES is “Overworld” from *Super Mario Bros. 3* (1998), composed by Koji Kondo. While many would choose the main theme from the original *Super Mario Bros.*, I believe “Overworld” is a better representative because it includes a demonstration of the capabilities of channel five with a frequently used “steel drum” sound sample:

<audio
	controls
	src="Super Mario Bros 3.mp3">
	Your computer does not support HTML in-line audio.
</audio>

> *[Listen on YouTube](https://youtu.be/Q_saM7I20pY)*

### The Game Boy

Nintendo released their next console in 1989, six years after the original release of the NES. This console was the Game Boy, an 8-bit handheld console. In a lot of ways, the Game Boy is a miniature NES, packing similar audio and visual tools into a 4-color screen with half the resolution (166x140) of the NES (256x240). The Game Boy’s APU followed in the footsteps of its predecessor, giving developers four analog channels with a bit depth of four. All of the Game Boy derivative models, including the Game Boy Color, have the same audio capabilities. My research on the Game Boy was primarily informed by the GB Dev Wiki’s page on Gameboy Sound Hardware[^gbdev]. Audio on the Game Boy was programmable with a tool called MusyX (pronounced *musics*) developed by a third-party studio called Factor 5[^factor5]. Factor 5 would go on to work on audio tools and games for Nintendo’s later consoles as well.

The first two sound channels on the Game Boy are pulse waves. Each channel can produce four different duty cycles and comes equipped with an individual volume envelope. The volume envelopes on the GB offer adjustable linear volume increase or decrease. The first pulse channel has a frequency sweep unit similar to that of the NES. The GB does not have a triangle wave channel. Channel three is a noise generator that employs a very similar noise generator to that of the NES. While the Game Boy also has a noise mode switch, mode 1 in the GB continues to exclusive-or bits 0 and 1 and instead places the result in bit six as well as bit 14, creating a 127-step noise sequence. It is unknown whether this difference was intentional or not. 

<audio
	controls
	src="Links Awakening.mp3">
	Your computer does not support HTML in-line audio.
</audio>

> *An example of noise mode 1 on the Game Boy is the "bonk" sound from The Legend of Zelda: Link's Awakening.*

The Game Boy’s fourth channel is a delta modulation channel that is a fair bit more advanced than that of the NES. The GB DMC comes equipped with a 32-byte wave table that stores a waveform as  64-sample, 4-bit PCM. One weakness of this system is that hot-swapping the values in the wave table will cause artifacts in the sound Game Boy carts could store up to 4MB, four times the capacity of the largest NES carts, making the use of the DMC significantly more common. Since the GB lacked a triangle wave channel, many developers (such as Hip Tanaka, composer for Super Mario Land) chose to use it to add in another basic waveform, but one iconic example of DMC ingenuity is the “pika!” voice sample played on the title screen of Pokémon Yellow, voice acted by the same actor who voices Pikachu in the Pokémon anime, Ikue Ootani:

<audio
	controls
	src="Pokemon Yellow.mp3">
	Your computer does not support HTML in-line audio.
</audio>

While the Game Boy did not have expansion chips, Nintendo left in the capability for expansion audio with a fifth audio channel that takes an analog audio signal from the game cartridge[^chipmusic]. There are no known examples of an official Game Boy game making use of this feature. However, with the Game Boy’s prominent place in the chiptune music scene, this input channel has received the attention it deserves in the form of Nanoloop Mono, an analog synthesizer in the form of a Game Boy cartridge[^oliverwittchow]. Another notable Game Boy homebrew creation is Little Sound Dj, an extremely popular chiptune composition program in the form of a Game Boy ROM.

One reason the Game Boy is favored over the NES by chiptune music composers (besides the obvious benefit of portability) is that the Game Boy is capable of stereo audio! Each channel DAC was capable of sending its audio to the left channel, the right channel, or both. While the Game Boy’s built-in speaker is monaural, the 3.5mm headphone jack outputs stereo audio.

I’ve chosen “Birabuto Kingdom” from *Super Mario Land*, composed by Hip Tanaka, to represent the Game Boy. Despite *Super Mario Land* being a Game Boy launch title, this song demonstrates almost every exciting feature of the GB APU, with the percussion loop moving in stereo and the DMC generating a triangle wave to fill in the bass part. Any discussion of Nintendo game audio would be incomplete without the work of Hip Tanaka, who stood toe-to-toe with the revered Koji Kondo in compositional skill, ingenuity, and legacy.

> *For more on Hip Tanaka, I highly recommend listening to [“The Music of Hip Tanaka” by The Frame Savers](https://soundcloud.com/theframesavers/tfs-pocket-43-the-music-of-hip-tanaka).*

<audio
	controls
	src="Super Mario Land.mp3">
	Your computer does not support HTML in-line audio.
</audio>

> *[Listen on YouTube](https://youtu.be/Gb33Qnbw520)*

### The Super Nintendo Entertainment System

The next decade was truly an age of innovation, and Nintendo’s ‘90s console was no exception. In 1991, Nintendo released the Super Nintendo Entertainment System, a 16-bit console packed with one of the most powerful audio subsystems the gaming world had ever seen. More complex audio synthesis became possible in the 16-bit era as memory prices fell significantly. Sega’s 16 bit console, the Genesis, is revered for its FM synthesis sound engine (with six channels that can each produce four sine waves), but Hudson’s PC Engine chose to go the route of wavetable synthesis, leaving the later-released SNES to choose what route it would go.

Nintendo’s Ken Kutaragi, a true visionary in console design, was in charge of creating the SNES audio system. What he created was not just a chip and architecture, but rather an incredibly complex audio subsystem called the Nintendo S-SMP[^fatnick]. The S-SMP is a revolutionary wavetable sound system based around a Sony SPC700 CPU, with its own internal register, 64kB of RAM, and a 16-bit DSP chip[^datschge].

Thanks to Kutaragi’s S-SMP, the SNES is capable of playing 8 wavetable synthesis voices at the same time, with 8-bit panning per channel allowing extremely precise stereo sound design, all with 8-bit depth at 32kHz. This system operated with 32-sample Adaptive Delta PCM wavetable samples stored in a custom 9-bit format (16 9-bit values composed of a 1-bit header and two 4-bit samples), designed by Kutaragi to increase compression and allow lower-amplitude samples to be encoded in higher quality by adapting the quantization factor every 16 samples[^spc700ref] [^snesdevmanual]. The main benefit of the S-SMP over the FM synthesis sound chip of the Genesis is the variety of different sounds that wavetable synthesis can employ. Additionally, the S-SMP was easier to program for, as it allowed developers to write their own song playback engine microcode as they see fit.

<audio
	controls
	src="Megaman X3.mp3">
	Your computer does not support HTML in-line audio.
</audio>

> *To understand the scope of the S-SMP’s variety, compare Mega Man X3’s “Crush Crawfish” to the samples from Super Mario World. [Listen on YouTube](https://youtu.be/lbrSG6Hyf0Y)*

The S-SMP’s wavetable synthesis is supplemented by a small library of effects. The most iconic SNES effect is the SNES’ echo unit, which is capable of applying an echo to any of the SNES’ audio channels with adjustable delay, feedback, pan, and EQ[^snesdevmanual]:

<audio
	controls
	src="Super Mario World Underground.mp3">
	Your computer does not support HTML in-line audio.
</audio>

> *Listen to the iconic SNES echo in Super Mario World’s underground theme. [Listen on YouTube](https://youtu.be/M7G--2s3bdc)*

The SNES also had a single noise generator, which I can only assume is identical to the mode 0 LFSR in the NES and Game Boy. There is only one noise generator, but it can be applied to any number of channels. The SNES also offered frequency modulation-based pitch modulation of channels. The pitch modulation unit could frequency modulate one channel based off of the changes in frequency of another channel (note that this means that for every channel that is modulated, another channel is unavailable)[^snesdevmanual]. Finally, every channel was equipped with a unique volume envelope, capable of applying linear or curved growth or decay or a traditional ADSR filter.

Like the Game Boy, the SNES is capable of taking additional audio from the cartridge, but this time in stereo[^caitsith2]. These audio pins are used for most of the SNES’ add-ons, including the Super Game Boy, an attachment that allows playing Game Boy games through the SNES on a television, and the BS Satellaview, an internet-connected extension that allowed games and special content to be distributed periodically a la television programming. Cartridge audio in likely would have been used for the never-released SNES CD, one of Ken Kutaragi’s less successful projects.

My song choice to represent the SNES in the *Super Mario* franchise is “Overworld” from *Super Mario World*, composed by Koji Kondo. This song uses a variety of unique sounds, including a steel drum similar to the one used in *Super Mario Bros. 3*, and demonstrates Koji Kondo’s vision of the "Mario sound."

<audio
	controls
	src="Super Mario World Overworld.mp3">
	Your computer does not support HTML in-line audio.
</audio>

> *[Listen on YouTube](https://youtu.be/Fn0khIn2wfc)*

### The Virtual Boy

Nintendo’s next console was truly a child of the spirit of ‘90s innovation. The Nintendo Virtual Boy, released in 1995, is a 32-bit home console designed to play 3D VR games with seperate screens built into the console for each eye instead of a TV output. For audio, it was equipped with stereo speakers and a stereo headphone jack. While this console was absolutely revolutionary, it completely failed due to continuously lowered project budget, repeated cuts of promised features, an extremely small library of games (22 to be exact, with even less released in the US), and 3D technology that wasn’t quite advanced enough to impress consumers. Thanks to the Virtual Boy’s status as a sort of cult favorite, it was by far the most well-documented console within the scope of my research, with sites like Planet Virtual Boy having thorough memory maps and archives of official Nintendo documents in fair supply.

The Virtual Boy’s audio system is loosely similar to the S-SMP. It is capable of playing 10-bit, 41.7kHz audio from five wavetable synthesis channels and one noise generator channel[^guyperfect]. However, the Virtual Boy’s maximum cart size of 2MB meant that VB games could not use as many different samples as SNES games often did [^planetvb]. The VB’s wave tables, one for each of the five wave channels, stored 32-sample, 6-bit PCM waves[^vbdevmanual]. A notable drawback of the VB APU is that the wave tables cannot be written to unless every sound channel is disabled. Each channel is equipped with a linear increase or decrease volume envelope and 4-bit stereo spread. The last wave channel has a unit that can perform linear frequency sweep or frequency modulation based on a wave stored in a separate modulation RAM bank[^vbdevmanual]. The sixth audio channel on the VB is a noise generator. While the generator uses the same LFSR as other consoles, the Virtual Boy had eight distinct noise modes, different based on what bits were exclusive-or’d, allowing a wide spectrum of noise tones.

The Virtual Boy had pins for stereo audio input and output from the cartridge[^projectvb]. It is unknown if these were ever used, but given the extremely small library of games, lack of extension peripherals, and the number of promised features that the Virtual Boy failed to deliver on, the odds of their use are extremely low.

The only *Mario* games released on the Virtual Boy were spinoffs including *Mario’s Tennis* (not to be confused with *Mario Tennis* for the Game Boy Color) and *Mario Clash* (a unique, 3D take on classic *Mario Bros.* gameplay), so I’ve chosen a sample from *Virtual Boy Wario Land*, composed by Kazumi Totaka, to represent this console. Stage 2’s theme makes ample use of the envelopes and pitch modulation features of the Virtual Boy.

> *Inline recording coming soon. [Listen on YouTube](https://youtu.be/TZ227-W0kto)*

### The Nintendo 64

Nintendo’s next full-feature console was the Nintendo 64, a 1996 64-bit home system. While the N64 offered an incredible gaming experience with its early 3D titles, its audio systems are somewhat lacking. There is no dedicated audio processing system on the N64, leaving many to regard it as a step down from the Super Nintendo. Nintendo insists that the software-based audio on the N64 allows greater flexibility, which is not untrue, but the lack of dedicated audio processing hardware means audio dips into the console’s processing time, restricting what developers were able to create[^n64audiodevmanual]. While the N64 boasted the ability to play up to 100 sound channels at once, the processing time cost of audio on the N64 is rather severe, with even Nintendo admitting that “the approximate time required per voice with a playback rate of 44.1 KHz is estimated to be 1% of RSP time,” thereby making channel counts above 15 often unfeasible[^nextgeneration] [^n64audiodevmanual]. The Nintendo 64 is programmable in C, a much-needed jump from the ASM used by previous consoles. The N64’s DAC is designed with 33kHz audio in mind, but is capable of playing other rates of audio as well[^n64audiodevmanual]. The N64 offers 16-bit stereo and bit depth.

The N64 was designed with a variety of audio methods in mind, including raw audio playback, wavetable synthesis, and MIDI. Nintendo’s insistence on sticking with cartridge-based console design benefitted load times but seriously hampered storage capabilities, giving the N64 only up to 64MB of storage compared to the 700+ MB stored in a PlayStation game’s standard CD-ROM, and essentially rendering raw recorded audio an impossibility for the N64. Wavetable synthesis was a reasonable option for storage concerns and was what many games employed. The N64 was capable of playing 16-bit uncompressed PCM or compressed AIF-C ADPCM files, and the console touted a special ADPCM “N64 Compression Format” that stored audio in roughly 1/4th its original size without sacrificing quality[^n64audiodevmanual].

Most N64 games, however, used MIDI to generate their sound. The N64 is capable of using type 0 general MIDI files (and can convert type 1 MIDI to type 0 internally), but it also offered a special “compact MIDI” format unique to the N64. MIDI programming on the N64 was aided by the return of Factor 5’s MusyX software.

The N64’s audio programming library comes with a number of delay line-based effects, including small and large room reverb, delay-line echo, flange, chorus, LPF, and any custom effects developers wrote, all adjustable in programming[^n64programmingmanual].

> *“Giali Theme” from The New Tetris, composed by Neil Voss, demonstrates some of these effects. [Listen on YouTube](https://youtu.be/kfg4l6Aafw4)*

There are also oscillator functions for pitch vibrato and tremolo to compliment the availability of MIDI pitch bend. Like the consoles before it, the N64 was equipped with a stereo audio pinout on the cartridge[^dextrose]. This likely would have been used for the 64DD, a cancelled disc drive peripheral for the N64, and the Wideboy 64, a never-released N64 version of the Super Game Boy. On the topic of failed peripherals, only two games on the Nintendo 64 were compatible with the N64 VRU, or Voice Recognition Unit, *Hey You, Pikachu!* And *Densha De Go! 64*. The VRU is a microphone capable of simple speech recognition.

There is no game more iconic to the Nintendo 64 than *Super Mario 64*, and no song more iconic to Super Mario 64 than “Bob-Omb Battlefield,” composed by Koji Kondo.	This song unmistakably has the “sound” of MIDI, and clearly demonstrates the increase in sound quality compared to the Super Nintendo, but comes across as dated and tinny where the Super Nintendo had an iconic and unique sound that represents a clear understanding and willingness to work with the system’s capabilities.

> *[Listen on YouTube](https://youtu.be/YKtFsLyz6Zo)*

### The Game Boy Advance

The next Nintendo handheld on the market was the Game Boy Advance. Unlike the Game Boy Color systems, the GBA presented an entirely new and revamped experience rather than just further expanding the Game Boy’s capabilities. Released in 2001, the GBA is a portable 32-bit console with capabilities generally similar to the Super Nintendo. Games on the GBA could be up to 32MB, but most games were 8MB. The console had a mono speaker and stereo headphone jack ( The Game Boy Advance SP, the second revision of the GBA, required an adapter to 3.5mm for headphones to be used).

The console sports a DAC that outputs stereo 9-bit audio at 32.768kHz (or, optionally, a different “ratio” of depth and rate). However, audio actually leaves the console via 1-bit, 16.78MHz (the GBA CPU’s clock speed) pulse width modulation. At 32.768kHz, this meant a total of 512 pulses are sent per audio sample. In a sense, the GBA simulated 9-bit samples as the average of N low voltage samples and 512-N high voltage samples. The pulse width modulation output is smoothed by the console’s capacitors, speakers or headphone amp, and human ears to sound like the original bit depth and sample rate[^martinkorth]. GBA sound is programmable with Factor 5’s MusyX[^nwrstaff].

The GBA APU has six sound channels. The first four are a near-exact replica of the four analog channels on a Game Boy, with the only difference being that the 64-sample DMC wave bank could be split into two 32-sample banks to allow dynamic switching without noise artifacts[^martinkorth]. These channels were included because the Game Boy Advance can play original GB and GBC games. The other two channels, channels A and B, offer the ability to play back 8-bit digital samples. These channels each have storage for only 4 8-bit samples at a time, but use direct memory access techniques to quickly bring in more data on the fly. While the 8-bit digital capabilities of the GBA are a major step up from the 4-bit samples used on older consoles, the wave channels are limited to left-right-center stereo and can only play at either 100% or 50% of the original sample’s volume[^belogic].

Due to the combination of 8-bit digital samples with analog waveforms and the tone that pulse width modulation output gives the console, the Game Boy Advance is remembered for having an extremely unique sound with a very distinct amount of tinniness and buzz.

> *An excellent example of the “GBA Sound” is “Gravity” from Mega Man Zero 2, composed by Ippo Yamada, Masaki Suzuki, Luna Imegaki, Chicken Mob and Tsutomu Kurihara.* [Listen on YouTube](https://youtu.be/NeW0YpKZDKQ)


Few songs demonstrate this better than my pick for Super Mario representative of the Game Boy Advance, “Come On!” from Mario and Luigi: Superstar Saga, composed by Yoko Shimomura.

> [Listen on YouTube](https://youtu.be/NQEf2Cy_TlA)

### The GameCube

Later in the same year, Nintendo released its next home console, the GameCube. The GameCube’s most notable feature is that it left cartridges behind in favor of proprietary 1.5GB MiniDVD discs. The GameCube can output between 32kHz and 48kHz 16-bit stereo sound from up to 100 channels or 64 3D audio channels[^bourdon]. Additionally, it sports Dolby Pro Logic II, software that can turn stereo audio into 5.1 surround[^lalshimpi].

The GameCube’s audio system was designed by Factor 5, who also continued to provide MusyX for the console[^nwrstaff]. A custom Macronix 16-bit DSP chip with its own dedicated RAM and ARAM (“audio RAM”) is integrated into the ATI “Flipper” GPU[^lalshimpi]. The GCN took its audio development methodology cues from the Nintendo 64, giving developers free reign to write their own audio microcode system to play back audio in a way that works with their development needs and style[^changetal]. However, common-use microcodes were available for developers, including the AX μcode (included in the GC Development library), the Zelda μcode (so called due to its origin in the GCN *Legend of Zelda* games), and the JAC μcode (an earlier version of the Zelda μcode)[^bourdon].

The AX μcode is the most thoroughly studied thanks to the efforts of the team behind Dolphin, a GameCube and Wii emulator. In AX, the CPU,  μcode registers, RAM, ARAM, and audio pipeline send back and forth audio data (including channel numbers, effects, and properties like pan and volume), interrupts, and requests (to move, send, or replace data) on 5ms intervals, but audio data can be updated on a per-millisecond basis with predeclared updates[^bourdon].

The GameCube had a microphone peripheral that was only ever compatible with five games. It could be used to detect volume, often done in *Mario Party 6* and *7* minigames that encouraged blowing into the mic, detect pitch, as in the rhythm game *Karaoke Revolution Party*, or even recognize speech, such as in *Odama* or *Chibi-Robo!*[^giantbomb].

While 1.5GB of space was a major upgrade for audio developers, it still wasn’t always enough for high-quality recorded audio, especially with how much space of that 1.5GB is taken up by increasingly high-resolution 3D model textures. Thus, MIDI-like systems were often used for GameCube games. Due to the variable nature of GCN audio, specific information is relatively scarce, but it is likely that the GameCube uses similar AIF-C audio to other Nintendo consoles given that the audio file suffix for the GCN is “.ACF,” according to GameCube memory and software documentation, likely with 32- or 64-bit precision[^groepaz].

The GameCube’s library is full of a variety of *Super Mario* titles, but few are more memorable than *Super Mario Sunshine*. *Sunshine* evolved the 3D Mario format created in *Super Mario 64* with a gorgeous, bright, and unique world along with special gameplay mechanics. Koji Kondo’s compositions for *Sunshine* reflect the game’s fun, tropical attitude. “Staff Roll” is a cross between a victory romp, samba, and futbol fan anthem, all wrapped up in the final repetition of the game’s main musical motifs. Additionally, this track employs an extremely wide variety of sampled instruments, showcasing the capabilities of the GameCube’s audio system and storage capacity quite nicely.

> [Listen on YouTube](https://youtu.be/d_ehfRfkS7g)

### The Nintendo DS

The Nintendo DS, or Double-Screen, released in 2004. It was a portable console with not one, but two, screens, one of which was a touch screen. The DS uses game cards, similar to common SD cards, that could store anywhere from eight to 512 MB of data. The console has stereo speakers positioned to either side of the top screen and a stereo headphone jack. Sound in the DS is generated at a peak sample rate of 1.04MHz, bit depth of 24, but resampled for output to 32.768kHz, 10 bits using pulse width modulation[^martinkorth].

The DS has 16 variable sound channels. Every channel is capable of playing back digital audio in the form of 8- or 16-bit PCM or 4-bit IMA-ADPCM (The ADPCM standard developed by the International Multimedia Association) that decodes into PCM16. Each channel has 7-bit volume and 7-bit stereo pan, and while there are no built-in effects or envelope capabilities, these can be added in software. Channels 8-13 (counted starting with 0) are also capable of playing pulse waves with eight different duty cycle settings. Channels 14 and 15 can play noise. While the noise production algorithm is the same as in previous consoles (with only mode 0), the LFSR is actually emulated in software with programmed bitwise math functions[^martinkorth]. These analog sound channels are necessary because the original DS is capable of playing Game Boy Advance games.

In addition to these audio outputs, the Nintendo DS has a built-in microphone. Oliver Boudeville notes that the DS has the capability for “some limited speech-recognition”[^osdl]. I could not find any details on the microphone, but I suspect based on the size that it is a MEMS, or micro-electromechanical system, microphone.

2D *Mario* took a break during the Game Boy Advance era, but returned strong in *New Super Mario Bros. (DS)*, a title that combined classic *Super Mario* platforming gameplay with modern design sensibility. The overworld theme from NSMB, composed by Hajime Wakai, is my choice to represent the DS. “Overworld” is a wonderful earworm and clear demonstration of just how much the DS improved audio compared to the GBA.

> [Listen on YouTube](https://youtu.be/-GK41pLUuP0)

### The Nintendo Wii

The final console in the scope of this paper is Nintendo’s Wii. Released in 2006, the Wii revolutionized gaming and handily outside Sony and Microsoft’s consoles of the era. Despite being little more than a souped-up GameCube under the hood, it offered unique gameplay with motion controls and universally accessible games like *Wii Sports* that made the console a hit. The Wii used DVD-ROM style discs capable of storing either 4.7 or 8.5GB of data, far outclassing the previous generations’ storage capabilities. Finally, 23 years after the release of the Nintendo Entertainment System, real, recorded, full songs were practical!

The Wii’s audio subsystem is largely the same as the GameCube’s, sporting a similar DSP-in-GPU, microcode-based setup with only a few minor differences. The Wii has no dedicated ARAM for the audio system, but offers more RAM for the system in general, and has the potential for more total audio channe[^jmc47myth].

One unique audio feature of the Wii is that the controller, commonly referred to as a Wiimote, has a built-in speaker, allowing for direct audio feedback for player actions and more audiological immersion in games than lone stereo can provide. I was not able to find any specifications for the speaker, but based on photos and experience I can say that it is monaural, with a roughly 10mm driver, and extremely tinny and low quality due to the clearly cheap part and the lack of physical isolation for the speaker in the controller housing.

To represent *Super Mario* on the Wii, I believe that there is truly only one choice. *Super Mario Galaxy’s* “Gusty Garden Galaxy,” composed by Koji Kondo, is revered as one of the greatest pieces of video game music ever written. *Super Mario Galaxy’s* soundtrack features a recorded symphony orchestra, bringing an unprecedented level of depth and complexity to *Super Mario* series music.

> *I encourage you to leave this song playing as you read this paper’s conclusion for the sake of making the conclusion feel a bit less dismal.* [Listen on YouTube](https://youtu.be/VEIWhy-urqM)

### Conclusions

The content of this paper ceases following the Wii due to the complete lack of substantial information regarding Nintendo’s more recent releases, the 3DS, Wii U, and Switch. Finding any information at all regarding the Wii was a significant challenge. With the passing of each console generation information became more scarce throughout the research process for this paper, and nearly every single piece of substantial information I was able to gather for this paper was available only due to the hard work of emulator developers, homebrew game makers, romhackers, hardware modders, and retro console enthusiasts. Even the official Nintendo documents I used were only accessible thanks to gaming historians’ archival work. Research on gaming consoles would hardly be possible without the work of individual enthusiasts and does not exist without complaint from the companies that make these consoles.

Recently, Nintendo forcefully shut down Emuparadise, a website that hosted and shared thousands of retro games that Nintendo had abandoned. They did this so that they could make a profit on the 32 NES games they offer as a part of Nintendo Switch online, barely even a fraction of the entire library of NES games, the rest of which Nintendo has done nothing to preserve. The retro gaming community has spent uncountable hours preserving, collecting, analyzing, and sharing data and research on video games, and has been fought at every step of the way by gaming companies’ rights lawyers looking to monopolize access to only the few games they deem profitable. While this paper was premised as a historical analysis and summary without a central thesis, my conclusion is thus: The secrecy and monopoly employed by capitalist competitors in the games industry to “stay ahead” ruins the ability of researchers, homebrew developers, and enthusiasts to study, share, and learn more about video games.

> *View the full bibliography [here](/vgaudio/nintendium/bibliography).*

[^nesdevwiki]: NES DEV Wiki: NES Info, Programs, and Demos. “APU” [wiki.nesdev.com/w/index.php/APU](https://wiki.nesdev.com/w/index.php/APU)
[^greathierophant]: Great Hierophant, Nerdly Pleasures: You Say Obsessed as if it is a Bad Thing (07/31/15). “The Famicom Microphone - Obscure Functionality” [nerdlypleasures.blogspot.com/2015/07/the-famicom-microphone-obscure.html](http://nerdlypleasures.blogspot.com/2015/07/the-famicom-microphone-obscure.html)
[^factor5]: Factor 5 Development Studio, archived by archive.org. “MusyX - Audio Tools For Nintendo 64 And Game Boy” [archive.org/details/MusyXAudioToolsForNintendo64AndGameBoy/page/n9](https://archive.org/details/MusyXAudioToolsForNintendo64AndGameBoy/page/n9)
[^gbdev]: Various authors, Gameboy Development Wiki. “Gameboy Sound Hardware” [gbdev.gg8.se/wiki/articles/Gameboy_sound_hardware](http://gbdev.gg8.se/wiki/articles/Gameboy_sound_hardware)
[^chipmusic]: Various authors, Chipmusic. “The DMG’s 5th Sound Channel?” [chipmusic.org/forums/topic/7071/the-dmgs-5th-sound-channel/](https://chipmusic.org/forums/topic/7071/the-dmgs-5th-sound-channel/)
[^oliverwittchow]: Oliver Wittchow, Nanoloop: Music in Two Dimensions. “Nanoloop Mono” [nanoloop.com/mono/index.html](http://nanoloop.com/mono/index.html)
[^fatnick]: Fatnick, Skirmish Frogs blog site. “The Mysterious Legacy of the SNES Sound Chip” [skirmishfrogs.com/2016/08/22/the-mysterious-legacy-of-the-snes-soundchip/](https://skirmishfrogs.com/2016/08/22/the-mysterious-legacy-of-the-snes-soundchip/)
[^datschge]: “Datschge,” SNESmusic.org: The Music Archive. “How Sound on the SNES works” [snesmusic.org/files/spc700.html](http://snesmusic.org/files/spc700.html)
[^spc700ref]: Various authors, SFC Development Wiki. “SPC700 Reference” [wiki.superfamicom.org/spc700-reference](https://wiki.superfamicom.org/spc700-reference)
[^snesdevmanual]: Nintendo, archived by archive.org. “SNES Development Manual” [archive.org/details/SNESDevManual/page/n151](https://archive.org/details/SNESDevManual/page/n151)
[^caitsith2]: CaitSith2, caitsith2 personal webpage. “SNES Cart Chip Pinouts” [caitsith2.com/snes/flashcart/cart-chip-pinouts.html](https://www.caitsith2.com/snes/flashcart/cart-chip-pinouts.html)
[^guyperfect]: Guy Perfect, planetvb.com. “VB Sacred Tech Scroll - Virtual Boy Specifications.” [planetvb.com/content/downloads/documents/stsvb.html#virtualsoundunitvsu](https://www.planetvb.com/content/downloads/documents/stsvb.html#virtualsoundunitvsu)
[^planetvb]: Various authors, Planet Virtual Boy: Got Parallax?. “Hardware” [planetvb.com/modules/hardware/?type=vb&sec=specs](https://www.planetvb.com/modules/hardware/?type=vb&sec=specs)
[^vbdevmanual]: Nintendo, archived by Planet Virtual Boy: Got Parallax?. “Virtual Boy Development Manual” [planetvb.com/content/downloads/documents/Virtual%20Boy%20Development%20Manual.pdf](https://www.planetvb.com/content/downloads/documents/Virtual%20Boy%20Development%20Manual.pdf)
[^projectvb]: ---, Project: Virtual Boy. “Cartridge Pinout” [projectvb.com/tech/cartpinout.html](http://www.projectvb.com/tech/cartpinout.html)
[^n64audiodevmanual]: Nintendo, archived by ultra64.ca. “Nintendo 64 Audio Development Guide” [ultra64.ca/files/documentation/nintendo/Nintendo_64_Audio_Development_Guide_NUS-06-0151-001A.pdf](https://ultra64.ca/files/documentation/nintendo/Nintendo_64_Audio_Development_Guide_NUS-06-0151-001A.pdf)
[^nextgeneration]: Next Generation, issue 24 (Dec 1996), archived by archive.org. p. 78 - N64 technical specifications [archive.org/stream/NextGeneration24Dec1996/Next_Generation_24_Dec_1996#page/n75/mode/2up](https://archive.org/stream/NextGeneration24Dec1996/Next_Generation_24_Dec_1996#page/n75/mode/2up)
[^n64programmingmanual]: Nintendo, archived by n64devkit.square7.ch. “Nintendo 64 Programming manual” [n64devkit.square7.ch/pro-man/index.htm](http://n64devkit.square7.ch/pro-man/index.htm)
[^dextrose]: “Dextrose,” icequake.net N64 information. “-N64 CART info-” [n64.icequake.net/mirror/www.crazynation.org/N64/](http://n64.icequake.net/mirror/www.crazynation.org/N64/)
[^martinkorth]: Martin Korth, hosted by akkit.org. “GBATEK: Gameboy Advance / Nintendo DS - Technical Info - Extracted from no$gba version 2.5” [akkit.org/info/gbatek.htm](http://www.akkit.org/info/gbatek.htm)
[^nwrstaff]: NWR Staff, NintendoWorldReport (03/03/2001). “GameCube FAQ, Factor 5” [nintendoworldreport.com/guide/1798/gamecube-faq-factor-5](http://www.nintendoworldreport.com/guide/1798/gamecube-faq-factor-5)
[^belogic]: Belogic, belogic.com. “The Audio ADVANCE: GBA Development for the Masses” [belogic.com/gba/](http://belogic.com/gba/)
[^bourdon]: Pierre Bourdon, LSE Blog: Operating Systems, Computer Security, Languages Theory, and Even More! (12/03/2012). “Emulating the Gamecube Audio Processing in Dolphin” [blog.lse.epita.fr/articles/38-emulating-the-gamecube-audio-processing-in-dolphin.html](https://blog.lse.epita.fr/articles/38-emulating-the-gamecube-audio-processing-in-dolphin.html)
[^lalshimpi]: Anand Lal Shimpi, AnandTech (07/12/2001). “Hardware Behind the Consoles - Part II: Nintendo’s GameCube” [anandtech.com/show/858/7](https://www.anandtech.com/show/858/7)
[^changetal]: Chang, Kyusik & Kim, GyuBeom & Kim, Taeyong. (2007). Video Game Console Audio: Evolution and Future Trends. 97 - 102. 10.1109/CGIV.2007.87. [researchgate.net/publication/4270536_Video_Game_Console_Audio_Evolution_and_Future_Trends](https://www.researchgate.net/publication/4270536_Video_Game_Console_Audio_Evolution_and_Future_Trends)
[^giantbomb]: Various authors, Giant Bomb. “GameCube Microphone Support” [giantbomb.com/gamecube-microphone-support/3015-8090/games/](https://www.giantbomb.com/gamecube-microphone-support/3015-8090/games/)
[^groepaz]: Groepaz, GC Forever (23/12/2996). “Yet Another Gamecube Documentation (but One That’s Worth Printing)” [gc-forever.com/yagcd/](https://www.gc-forever.com/yagcd/)
[^osdl]: Oliver Boudeville, OSDL (07/17/2008). “A Guide to Hombrew Development for the Nintendo DS” [osdl.sourceforge.net/main/documentation/misc/nintendo-DS/homebrew-guide/HomebrewForDS.html#sound ](http://osdl.sourceforge.net/main/documentation/misc/nintendo-DS/homebrew-guide/HomebrewForDS.html#sound)
[^jmc47myth]: JMC47, Dolphin Emulator blog (07/21/2018). “Myth Debugging: Is the Wii More Demanding to Emulate than the GameCube?” [dolphin-emu.org/blog/2018/07/21/myth-debugging-wii-more-demanding-emulate-gamecube/](https://dolphin-emu.org/blog/2018/07/21/myth-debugging-wii-more-demanding-emulate-gamecube/)