## Vim Notes


### Buffers
- In VIM everything is a buffer
- Typical file editing softwares, load the file into a buffer and application edits the file in the buffer. When the save button is hit it is saved to the disk.
- In VIM editing happens directly on the buffer, saving rewrites the file or creates a new file.

## Modes
- Vim has two modes Insert and Normal Mode

## CheatSheet

- Use ^W / ^B to skip words till the next whitespace is found. (eg., don't if we do w here, it cursor stays at ').
- % - go to opening or closing braces
- { or } - to skip paragraphs, usefuly for iterating methods
- changing words
    1/ * the word
    2/ g+n: highlights the word
    3/ c+g+n: change to new word
    4/ go to next occurence (n and . (repeat last command)

## References
- https://www.danielmsullivan.com/pages/tutorial_vim.html#:~:text=Vim%20has%20two%20main%20%22modes,spend%20most%20of%20your%20time.

