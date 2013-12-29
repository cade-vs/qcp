# NAME

QCP -- Quick Quake Network Copy

# SYNOPSIS

    # sending files/directories
    qcp file1 file2 dir3...
  
    # receiving content (files/dirs/etc.)
    qcp

# DESCRIPTION

QCP sends files and directories over the local network segment without need 
to specify sending and/or receiving hostnames. It auto-discovers send/receive 
mode and the peer host. The main purpose is to transfer files between 
machines in the most simple way possible, i.e. with only specifying the files
needed to be send.

Currently it is not safe to be used on public networks and it does not 
provide authentication and encryption. 
(see TODO chapter below)

QCP uses tar to pack transferred data.
(see REQUIREMENTS chapter below)

# EXAMPLES

To send files you only need to give files/directories names as arguments:

    qcp file1 file2 files dir1 dir2...
  
The remote end does not require any arguments:

    qcp
  
It does not matter which side will be started first!

By default the server side is in listening mode and the client tries to 
connect to the server. You can change sides:

    # client side listens for server to connect on port 2233
    qcp -l 2233
    
    # server side connects to the client on port 2233
    qcp -e ipaddr:2233 files...
    
Both options -e and -l disable the broadcasting auto-discovery. This may
be used between firewalled networks etc.    

# REQUIREMENTS

Perl with few standard modules:

  * IO::Socket::INET;
  * IO::Select;

tar

No specific version of perl or tar is required, any recent one should 
be sufficient.

# TODO

* domain keys
* authentication (combine with domain keys?)
* encryption
* compression

# CREDITS

QCP was inspired by NCP (http://www.fefe.de/ncp/) which site also contributed
to the name with the suggestion for copying quake data files :))) thanks.

# GITHUB REPOSITORY

    https://github.com/cade-vs/qcp

    git clone git://github.com/cade-vs/qcp

# AUTHOR

    Vladi Belperchinov-Shabanski "Cade"

    <cade@cpan.org> <cade@biscom.net> <cade@datamax.bg>

    http://cade.datamax.bg
