# DTT (Daily TV Torrents) Ruby Interface
This package is a Ruby module and script to interact with the
Daily TV Torrents web service API (http://www.dailytvtorrents.org/)
from the command line

## Requirements
 * Ruby (Tested with MRI 1.9.2-p290)
 * The JSON gem (gem install json)

## Examples

### Basic (Single show)
    user@machine:$ dtt futurama

This outputs

    HD[x] 720[x] Futurama             S06E26 11 days ago

### Basic (Multiple shows)
A comma separated list of shows without any spaces

    user@machine:$ dtt futurama,cops,sons-of-anarchy,weeds

This outputs

    HD[x] 720[x] Futurama             S06E26 11 days ago
    HD[x] 720[x] Cops                 S24E02 43 hrs ago
    HD[x] 720[x] Sons of Anarchy      S04E02 6 days ago
    HD[x] 720[x] Weeds                S07E11 7 days ago

Add the --colors (or -c) flag for colored output shown below

![Colored Output](/scottydelicious/dtt/screenshots/with_colors.png "With Colors")
