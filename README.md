# midi
Reading and writing of MIDI messages with Go.

## Goals

- implementation of complete MIDI standard (live and SMF data)
- provide building blocks for MIDI applications
- stable API
- no dependencies outside the standard library
- small modular packages (see below)
- pure Go library (no C, no assembler) 

## Non-Goals

- constructing of MIDI time code messages
- dealing with the inner structure of sysex messages
- connection to MIDI devices (combine this lib with http://github.com/rakyll/portmidi or http://github.com/scgolang/midi )
- CLI tools

## Modularity

This package is divided into small subpackages, so that you only need to import
what you really need. This keeps packages and dependencies small, better testable and should result in a smaller memory footprint which should help smaller devices.

For reading and writing of live and SMF MIDI data io.Readers are accepted as input and io.Writers as output. Furthermore there are common interfaces for live and SMF MIDI data handling: midi.Reader and midi.Writer. The typed MIDI messages used in each case are the same.

## Perfomance

On my laptop, writing 1000 messages (noteon and noteoff; live)

    BenchmarkSameChannel            123132 ns/op  12000 B/op  3000 allocs/op
    BenchmarkAlternatingChannel     123166 ns/op  12000 B/op  3000 allocs/op
    BenchmarkRunningStatusDisabled  110989 ns/op  12000 B/op  3000 allocs/op

On my laptop, reading 1000 messages (noteon and noteoff; live).
("Samechannel" makes use of running status byte).

    BenchmarkSameChannel            351412 ns/op  12001 B/op  7000 allocs/op
    BenchmarkAlternatingChannel     425478 ns/op  14000 B/op  8500 allocs/op

## Documentation

see http://godoc.org/github.com/gomidi/midi

## Status

usable (beta)

    package                   API stable          complete
    ----------------------------------------------------
    midiwriter                yes                 yes
    midireader                yes                 yes
    smf                       yes                 yes
    smf/smfwriter             yes                 yes
    smf/smfreader             yes                 yes
    midimessage/channel       almost              yes
    midimessage/cc            yes                 yes
    midimessage/meta          almost              yes
    midimessage/realtime      yes                 yes
    midimessage/syscommon     yes                 yes
    midimessage/sysex         no                  yes
    midiio                    yes                 yes
    
	------- porcelain packages -------
    smf/smftrack              no                  no
    midihandler               no                  yes


[![Build Status](https://travis-ci.org/gomidi/midi.svg?branch=master)](http://travis-ci.org/gomidi/midi)

- Supported Go versions: 1.2-1.8.
- Supported OS/architecture: Should work on all OS/architectures that Go supports (is tested on Linux, but no OS specific code).

## License

MIT (see LICENSE file) 
