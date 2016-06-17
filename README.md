About
=====

nim-subviewer is a Nim module for parsing SubViewer subtitle files.

For the purpose of the examples, assume a file named ``example.sub`` exists 
and contains the following data::

    [INFORMATION]
    [TITLE]This is a title
    [AUTHOR]achesak
    [SOURCE]GitHub
    [PRG]SubRip
    [FILEPATH]/home/adam/subtitles
    [DELAY]0
    [COMMENT]extra text can go here
    [END INFORMATION]
    [SUBTITLE]
    [COLF]&HFFFFFF,[STYLE]bd,[SIZE]18,[FONT]Arial
    
    00:01:30.50,00:01:40.10
    This is the first example subtitle.
    
    25:23:12.20,25:23:20.45
    This is a second subtitle.[br]This is on a new line.

Examples:
    
    # Parse the data.
    var sub : SubViewerData = readSubViewer("example.sub")
    # The previous line could also have been done the following ways:
    # var sub : SubViewerData = parseSubViewer(readFile("example.sub"))
    # var sub : SubViewerData = parseSubViewer(open("example.sub"))
    
    # Loop through the subtitles and output the subtitle text:
    for subtitle in sub.subtitles:
        echo(subtitle.text)
    # Output:
    # This is the first example subtitle.
    # This is a second subtitle.
    # This is on a new line.
    
    # Output the start and end times of the second subtitle.
    var subtitle : SubViewerSubtitle = sub.subtitles[1]
    echo(subtitle.startTime) # Output: "25:23:12.20"
    echo(subtitle.endTime) # Output: "25:23:20.45"
    
    # Output the title, author, and style information.
    echo(sub.title) # Output: "This is a title"
    echo(sub.author) # Output: "achesak"
    echo(sub.color) # Output: "FFFFFF"
    echo(sub.style) # Output: "bd"
    echo(sub.size) # Output: "18"
    echo(sub.font) # Output: "Arial"

License
=======

nim-subviewer is released under the MIT open source license.