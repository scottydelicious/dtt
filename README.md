# DTT (Daily TV Torrents) Ruby Interface
This package is a Ruby module and script to interact with the
Daily TV Torrents web service API (http://www.dailytvtorrents.org/)
from the command line

## Requirements
 * Ruby (Tested with MRI 1.9.2-p290)
 * The JSON gem (gem install json)
 * wget

## Installation
Place the dtt script in a directory that is in your executable path, e.g. ~/bin/ or
/usr/local/bin/

## Examples
You can run dtt with the -h (or --help) flag to see a list of options. The
help screen is a work in progress at this point. All the options are listed,
but their descriptions may be unhelpful.

### Basic (Single show text info)
    user@machine:$ dtt futurama

This outputs

    HD[x] 720[x] Futurama             S06E26 11 days ago

\*\* Note: This is the same as dtt --show --text futurama (--show and --text are the default)

### Basic (Multiple shows text info)
A comma separated list of shows without any spaces

    user@machine:$ dtt futurama,cops,sons-of-anarchy,weeds

This outputs

    HD[x] 720[x] Futurama             S06E26 11 days ago
    HD[x] 720[x] Cops                 S24E02 43 hrs ago
    HD[x] 720[x] Sons of Anarchy      S04E02 6 days ago
    HD[x] 720[x] Weeds                S07E11 7 days ago

Add the --colors (or -c) flag for colored output shown below

![Colored Output](/scottydelicious/dtt/raw/master/screenshots/with_colors.png "With Colors")

### Episode
Get info on the latest episode of a show with the --episode (or -E) flag.
Returns last season/episode number, upload age, and available qualities.

    user@machine:$ dtt cops --episode

This outputs

    Latest Episode of cops is S24E02
    Uploaded 2 days, 1 hours, 48 minutes and 15 seconds ago
    Available in [HD] [720]

### Torrents (Get info on the torrent for a given quality)
Using the --torrent (or -T) flag you can get information on the healthiest
torrent for a given --quality (-q). The default --quality is HD which seems 
to be an HDTV rip encoded in SD widescreen resolutions. The available options
for --quality are hd, 720, and 1080. Not all formats are always available and
a local parse error is thrown if no results are found remotely.
    
    user@machine:$ dtt two-and-a-half-men -T

Produces the output

		name: Two_and_a_Half_Men_S09E01_HDTV_XviD-ASAP_[eztv]
		quality: hd
		age: 0 days, 1 hours, 48 minutes and 35 seconds
		data_size: 183534808
		seeds: 532
		leechers: 103
		link: http://www.dailytvtorrents.org/dl/de5/Two_and_a_Half_Men_S09E01_HDTV_XviD-ASAP_%5Beztv%5D.DailyTvTorrents.torrent

		Download this torrent? [y/N]

Entering "y" or "yes" will download the torrent to the current directory using wget.
Entering "n" or "no", or just pressing enter will exit as N is the default.

Specifying the quality with -q or --quality will grab info and offer to download
the healthiest torrent for that quality

    user@machine:$ dtt two-and-a-half-men -T -q 720

Will present info on the 720p torrent
		
		name: Two.and.a.Half.Men.S09E01.REPACK.720p.HDTV.x264-IMMERSE
		quality: 720
		age: 0 days, 0 hours, 14 minutes and 14 seconds
		data_size: 509753698
		seeds: 1
		leechers: 0
		link: http://www.dailytvtorrents.org/dl/dfq/Two.and.a.Half.Men.S09E01.REPACK.720p.HDTV.x264-IMMERSE.DailyTvTorrents.torrent

		Download this torrent? [y/N]

