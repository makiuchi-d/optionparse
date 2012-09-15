# Command line option parser for php

## Overview

A simple command line option parser inspired from powerful tool like
Console_CommandLine, without complicated functions.

This program is designed to work by single file and does not depend on
other libraries. There is only one thing required to use this parser
is include/require this file.

## Usage

    // create parser instance.
    $parser = new Optionparse(array(
        'name'        => 'yourprogram',
        'version'     => '1.0.0',
        'description' => 'Description of your program',
        'arguments'   => 'argument list',
        ));
    
    // exsample for the option which has associated argument.
    // the attribute 'help_name' is required.
    // hese styles are supported:
    //   -p/path/to/dir -p=/path/to/dir -p /path/to/dir
    //   --path=/path/to/dir --path /path/to/dir
    $parser->addOption('path',array(
        'short_name'  => '-p',
        'long_name'   => '--path',
        'description' => 'path to the dir',
        'default'     => '/tmp',
        'help_name'   => '/path/to/dir',
        ));
    
    // example for the boolean option.
    // this optoin cannot set string parameter.
    // these are declared as true:
    //   -v --verbose -vaaa -v=aaa --verboss=aaa
    // these are declared as false:
    //   -v- --verbose= -v=- --verbose=-
    $parser->addOption('verbose',array(
        'short_name'  => '-v',
        'long_name'   => '--verbose',
        'description' => 'turn on verbose output',
        ));
    
    // this parser does not have default options.
    // you need to add help/version, unlike Console_CommandLine.
    $parser->addOption('help',array(
        'short_name'  => '-h',
        'long_name'   => '--help',
        'description' => 'show this help message',
        ));
    
    // parse $argv.
    $options = $parser->parse();
    
    // this parser does not display help message automatically.
    if($options['help']){
        $parser->displayUsage();
        exit(0);
    }
    
    // non-option arguments are arranged into '_arguments_'.
    foreach($options['_arguments_'] as $arg){
        echo $arg, "\n";
    }

