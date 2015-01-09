{
    "title": "Perl",
    "description": "Using Perl to develop applications.",
    "date": "2014-02-01",
    "categories" : [
    	 "posts"
    ],
    "tags": [ "perl", "sdlc" ],
    "status": "research"
}

Have chosen to use Perl because;

* Perl is common in opensource projects and has extensive documentation and huge community
* there a [CMIS wrapper](https://github.com/MichaelDaum/cmis-perl) written in Perl
* there's a [DLNA media server extension](http://www.cybergarage.org/twiki/bin/view/Main/CyberLinkForPerl) written in Perl
* handles text stuff (which there is going to be heaps of)
* it was new to me and I like a challenge

Going to try and keep it neat and maintainable through the help of the Eclipse - Epic plugin.

## Steps

Never used perl before so [where do we begin](http://www.imdb.com/title/tt0066011/?ref_=nm_flmg_com_92)? At the [beginning](http://www.perl.org/books/beginning-perl/) I guess:

1. perl is an interpreted language (not compiled to a binary) so need an interpreter
1. get help
1. be good to the [environment](http://www.imdb.com/title/tt0497116/) variables
1. reuse, reduce, recycle - live sustainably with the Comprehensive Perl Archive Network
1. EPIC debugging is, well, [epic](http://www.imdb.com/title/tt0848537/)
1. document as you go, who would have thunk it
1. a [name by any other](http://www.imdb.com/title/tt0117509/) is conventional

### The Perl Interpreter

To check if already have a perl interpreter installed type the following into a command prompt:
 
```
    perl -v 
```

It should return something like:

```
    This is perl 5, version 12, subversion 4 (v5.12.4) built for darwin-thread-multi-2level
    (with 2 registered patches, see perl -V for more detail)
    
    Copyright 1987-2010, Larry Wall
    
    Perl may be copied only under the terms of either the Artistic License or the
    GNU General Public License, which may be found in the Perl 5 source kit.
    
    Complete documentation for Perl, including FAQ lists, should be found on
    this system using "man perl" or "perldoc perl".  If you have access to the
    Internet, point your browser at http://www.perl.org/, the Perl Home Page.
```

If it doesn't, [download one](http://www.perl.org/get.html) for the relevant platform:

|Platform  | Where |
|----------|-------------------|
|mac  | pretty likely already installed  |
|windows | could get [activestate](http://www.activestate.com) or [strawberryperl](http://strawberryperl.com) | 
|linux  | consult package manager |

Once have the perl interpreter installed have access to the [perl shell](http://www.perlmonks.org/?node_id=640489) with:

```
    perl -MCPAN -e shell   
    cpan  
```

### getting help

Perl is up to version 5 now and that means there is tons of help out there.  Some of the obvious places are;

* http://perldoc.perl.org/perl.html and http://www.perl.org/learn.html
* [Beginning Perl Intro](https://docs.google.com/viewer?url=http://blob.perl.org/books/beginning-perl/3145_Intro.pdf) explains about getting text: _typing `perldoc perl` from a command prompt will get you a table of contents and some basic infomration about Perl.  The pages your probably going to use are the Perl FAQ and 'perlfunc', which describes the built-in functions_.  Page 10 in here also lists help sources.
* http://www.perlmonks.org
* http://www.perlhowto.com
* these look really simple to go through if have a bit of time: http://docstore.mik.ua/orelly/perl3/lperl/index.htm and http://docstore.mik.ua/orelly/perl4/index.htm

As with all help / how-to's these established sources sometimes had varying levels of details for some of the start-up type questions like; @INC and the environment, working out what modules are installed or what to call things.  Usually had to put together a couple to get the answer (like the ones below).

### @INC

As start to use (pardon the pun), perl and edit first modules, a number of the errors popped up relating to modules that were 'using' but couldn't find.  This will probably be a path issue but the fix isn't that obvious as there are gazillions of different ideas out there like:  

* mixture of [use, '@INC' and PERL5LIB](http://stackoverflow.com/questions/2526804/how-is-perls-inc-constructed-aka-what-are-all-the-ways-of-affecting-where-pe)
* overview of [special variables](https://docs.google.com/viewer?url=http://blob.perl.org/books/beginning-perl/3145_AppB.pdf) like '%ENV', '@INC', '%INC'
* another environment setup [PERL5LIB](http://www.perlmonks.org/?node_id=867860)
* some more about [modules](https://docs.google.com/viewer?url=http://blob.perl.org/books/beginning-perl/3145_Chap10.pdf)
* [use(), require(), do(), %INC and @INC Explained](http://www.perl.com/pub/2002/05/14/mod_perl.html)

Somewhere in this list (start at the top and work down) and google will probably be the answer.

### CPAN Perl Modules

There are a gazilion [perl modules](https://docs.google.com/viewer?url=http://blob.perl.org/books/beginning-perl/3145_Chap10.pdf) or bits of code already written to do all sorts of things, so where is it?

* installed as part of the interpreter  (File::Find, benchmark etc)
* code up on repositories like GitHub
* perl package [repositories](http://docs.activestate.com/activeperl/5.10/faq/ActivePerl-faq2.html#ppm_repositories) like for ActiveState
* [Comprehensive Perl Archive Network](http://www.cpan.org/misc/cpan-faq.html) (CPAN)

I am using macOSX so perl was installed already and installed the cpan addon [package manager](http://www.bioperl.org/wiki/Tutorial:Installing_Perl_modules) by entering the [code below](http://search.cpan.org/~miyagawa/App-cpanminus-1.7001/bin/cpanm) in a terminal:

```
    sudo cpan App::cpanminus
```

Now [install](http://www.cpan.org/modules/INSTALL.html) any module you can find on cpan `sudo cpanm Module::Name`.

To find what modules are currently installed, as with most things perl there seems to be multitude of ways:

* `instmodsh` [to see all installed modules](http://www.cyberciti.biz/faq/how-do-i-find-out-what-perl-modules-already-installed-on-my-system/)
* `perldoc -l Net::UPnP` [to see if Net::UPnP is installed](http://www.perlhowto.com/list_the_installed_modules), this will show where the module (.pm) is
* `perl -MTie::Hash -e 1` [to see if Tie::Hash is installed](http://www.perlhowto.com/check_if_a_module_is_installed), this will run it so if not installed will get and error message and if installed then will need to break execution 
* see the `perlmodinstall` manpage

### EPIC

To get the most out of EPIC, need to install some supporting perl modules:

* project templates (Module::Starter)
* source formatting (Perl::Tidy), also get colouring
* best practice approach (Perl::Critic)
* syntax (Perl::Debugger and Pad::Walker)
* commenting / documentation ([perlpod](http://perldoc.perl.org/perlpod.html))
* eclipse perspective for outline views of code and consoles for heaps of things like tasks, logs etc

To do that we ran the following code:

```
    sudo cpanm Module::Starter
    sudo cpanm Perl::Tidy
    sudo cpanm Perl::Critic
    sudo cpanm Pad::Walker
```

When configuring these into [EPIC preferences](./Paint-by-numbers:-Eclipse-with-Epic-and-Egit) need to find where the modules installed to as couldn't use the default locations. 

### Perldoc

Understanding how perldoc works, in particular the syntax for embedding pod into code and then using it to auto-generate documentation was a great place to start understanding perl.  In doing this first, got to see code examples, work out how to see and fix mistakes like forgetting to put in spaces and semicolons at end of lines and had to use the perl interpreter and instal modules.  Also was an easy, practical way to start looking at the perl language, and actually got to produce something helpful.

Got some help from the following:

* http://search.cpan.org/~rjbs/perl-5.18.1/pod/perlpod.pod
* http://perldoc.perl.org/perlpod.html
* http://www.perlmonks.org/?node_id=252477

The first pod we did was inside one of the pDLNA modules:

* create some heading information for the package (remember the = operator needs to be against the margin no spaces and sometimes need space at the end of line to work properly)

```
=head1 NAME

package PDLNA::SSDP - core module for Simple Service Discovery Protocol (SSDP).

=head1 DESCRIPTION

When a Universal Plug and Play (UPnP) enabled device joins a network.....

=cut
```

* documentation for the functions used, note the use of `over`, `begin/end html`, `back` and `cut`, these give the pod structure (over to start the list and back to end it), also using html inside the pod meant could link between the resulting html docs, so when you [click](http://www.imdb.com/title/tt0389860/) on an internal library you get taken to the htmlpod for that module.  

```
=head1 LIBRARY FUNCTIONS

=over 12

=item internal libraries

=begin html

</p>
<a href="./Config.html">PDLNA::Config</a>,
<a href="./Database.html">PDLNA::Database</a>,
<a href="./Devices.html">PDLNA::Devices</a>,
<a href="./Log.html">PDLNA::Log</a>.
</p>

=end html

=item external libraries

L<IO::Socket::INET>,
L<IO::Socket::Multicast>,
L<Net::Netmask>.

=back

=cut
```

* the block of pod like the following gave chance to document as went the modules actions

```
=item add_receive_socket()

=cut
```

* this was how wrapped up pod in the module, note the use of `back` at start of the podblock below, this is to close off the headings above.  Note also the use of `L<<lt>...E<gt>>` this was a fiddly way to get the email link to work, the other web link was easier. 

```
=back

=head1 COPYRIGHT AND LICENSE

Copyright (C) 2010-2013 Stefan Heumader L<E<lt>stefan@heumader.atE<gt>>.

This program is free software: you can redistribute it and/or modify
it under the terms of the ......  If not, see L<http://www.gnu.org/licenses/>.

=cut
```

Once had put all the pod into the modules then created a perl program as below to generate html files like the one for [ssdp](../usefuldocs/SSDP.html).

```
    #!/usr/bin/perl
    
    use warnings;
    use strict;
    
    use Pod::Simple::HTMLBatch;
    use Pod::Simple::XHTML;

    my $in_dir = 'put directory in here';
    my $out_dir = $in_dir . 'POD';
    
    my $convert = Pod::Simple::HTMLBatch->new;
    $convert->html_render_class('Pod::Simple::XHTML');
    $convert->add_css('http://www.perl.org/css/perl.css');
    $convert->css_flurry(0);
    $convert->contents_page_start;
    $convert->contents_page_end;
    $convert->javascript_flurry(0);
    $convert->contents_file(0);
    $convert->batch_convert( [ $in_dir ], $out_dir );
```

### Some conventions

There seemed to be different naming conventions for different versions of perl but we're using:

* .pl for programs
* .pm for modules

This seems to be ok and works in the EPIC plugin to ensure that get nice syntax colouring.