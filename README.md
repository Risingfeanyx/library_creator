
##
super duper deprecated
go <a href="https://github.com/Risingfeanyx/Calibre_configs/blob/main/README.md" target="_blank">here</a> 

<h2>script to spin up a quick calibre instance </h2>


argument is 'lib_creator 'library you want to serve'

requires xvfb imagemagick

make sure to save books to the folder you're planning to create. 

all credit goes to https://calibre-ebook.com/

```
lib_creator()
{
        clear
        mkdir -p to_add_/"$1"
        mkdir -p library/"$1"
        #Calibre and its server instance requires a book, or book-esque file (cbz, pdf, mobi, epub, etc) to validate the server instance.
        wget http://www.gutenberg.org/ebooks/1342.kindle.noimages -O "$(pwd)"/to_add_/"$1"/pride.mobi
	read -rep "Calibre requires books in its directories to start. Press [Enter] key once you've dropped the books you want to serve into $(pwd)/to_add_/""$1"""
        xvfb-run calibredb add to_add_/"$1" --library-path library/"$1"
        rm -rf to_add_/"$1"
        echo "http://$(hostname -I)":8080| sed 's/ //g'
        calibre-server library/"$1"
}
```
