<!-- DO NOT EDIT: File generated by docs/Generate.sh -->

NAME
====

Net::Pcap::Dump - Write packets to file.

SYNOPSIS
========

    use Net::Pcap::Dump :short;
    use Net::Pcap::Linktype :short;
    use Net::Pcap::C_Buf :short;

    my $data = C_Buf.new(Buf.new([0x00, 0x01, 0x02, 0x03]));
    my $dump = Dumper.open('dump.pcap', Linktype::Ethernet, 1500);
    $dump.dump($data);

EXPORTS
=======

    class Net::Pcap::Dump;

:short trait adds export:

    constant Dump ::= Net::Pcap::Dump;

DESCRIPTION
===========



class Net::Pcap::Dump
---------------------

    Implements `pcap_dump_t`.

### Attributes

    $.pcap_dump  is rw  is OpaquePointer
      Pointer to the pcap_dump_t structure.

    $.pcap       is rw  is Net::Pcap
      Parent pcap_t structure.

### Methods

    .open(Net::Pcap $p, Str $fname) returns Net::Pcap::Dump
      Constructor for Net::Pcap::Dump. Calls pcap_dump_open($p, $fname).

    .open(Str $fname, Net::Pcap::Linktype $linktype, Int $snaplen) returns Net::Pcap::Dump
      Constructor for Net::Pcap::Dump. Calls pcap_open_dead and pcap_dump_open.

    .close()
      Closes the pcap_dump_t, and (if constructed by .open()) closes the parent pcap_t.

    .dump(Net::Pcap::C_Buf $data, Real $seconds)
      Write packet to file. Constructs a pcap_pkthdr_t with caplen and len from C_Buf.elems,
      and tv_usec and tv_sec from $seconds. Then calls pcap_dump on the data and the pcap_pkthdr_t
      structure.
