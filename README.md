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

It is not safe to be used on public networks unless encryption is used! 
See below for examples how to enable encryption.

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

To use symmetric cryptography:

    # use "www.bis.bg" as password
    qcp -s www.bis.bg
    
    # ask interactively for password
    qcp -s ask
    
    # use specific cypher
    qcp -s ask -S Twofish2

To use compression:

    # send
    qcp -z files...
    
    # receive
    qcp -z

# REQUIREMENTS

Perl with few standard modules:

  * IO::Socket::INET
  * IO::Select

tar

No specific version of perl or tar is required, any recent one should 
be sufficient.

For further features, other modules are required:

  * Term::ReadKey  -- used for safe password entry
  * Crypt::CBC     -- cryptography module
  
QCP uses the following cyphers (in this order):

  * Crypt::Twofish2
  * Crypt::Twofish
  * Crypt::Rijndael
  
# INSTALLING PERL, PERL MODULES AND REQUIRED SOFTWARE

Install required software and perl modules with debian apt-get:

    apt-get install perl
    apt-get install tar
    apt-get install libterm-readkey-perl 
    apt-get install libcrypt-cbc-perl
    apt-get install libcrypt-rijndael-perl
    apt-get install libcrypt-twofish-perl

Install required perl modules with CPAN:

    cpan Term::ReadKey
    cpan Crypt::CBC
    cpan Crypt::Rijndael
    cpan Crypt::Twofish
    cpan Crypt::Twofish2

# TODO

* domain keys
* authentication (combine with domain keys?)

# KNOWN PROBLEMS

If both sides are run in the same MODE (server/push or client/pull) and direct
listen (-l) and connect (-e) options are used, qcp will block. This will be
fixed in the future.

# CREDITS

QCP was inspired by NCP (http://www.fefe.de/ncp/) which site also contributed
to the name with the suggestion for copying quake data files :)) thanks.

# GITHUB REPOSITORY

    https://github.com/cade-vs/qcp

    git clone git://github.com/cade-vs/qcp

# AUTHOR

    Vladi Belperchinov-Shabanski "Cade"

    <cade@cpan.org> <cade@bis.bg> <cade@biscom.net> <cade@datamax.bg>

    http://cade.datamax.bg
