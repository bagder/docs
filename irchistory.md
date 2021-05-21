# History of IRC (Internet Relay Chat)

I've done my very best to gather information from as many sources as
possible to verify facts, stories and dates. If you have additional
information, have found errors in my text or just feel like commenting
anything, email me, submit an issue or post a pull-request!

Feel free to link to [this page](https://daniel.haxx.se/irchistory.html)
or host it elsewhere. Please keep me credited as author.

Other stories about [IRC history](http://www.irc.org/history.html).

## The Beginning

IRC was born during summer 1988 when Jarkko "WiZ" Oikarinen wrote the
first IRC client and server at the University of Oulu, Finland (where he
was working at the Department of Information Processing Science).

Jarkko intended to extend the BBS software he administrated at
tolsun.oulu.fi, to allow news the usenet style, real time discussions
and similar BBS features. The first part he implemented was the chat
part, which he did with borrowed parts written by his friends Jyrki
Kuoppala and Jukka Pihl. It was initially tested on a single machine,
and according to the words from Jarkko himself *"The birthday of IRC was
in August 1988. The exact date is unknown, at the end of the month
anyways."*. The first IRC server was named tolsun.oulu.fi.

Jyrki Kuoppala pushed Jarkko to ask Oulu University to free the IRC code
so that it also could be run outside of Oulu, and after they finally got
it released, Jyrki Kuoppala immediately installed a server (which later
became irc.cs.hut.fi). This was the first "irc network".

Ari Lemmke's own words: *"At the same time Jyrki installed ircd, I was
at the same room and had nothing to do, so I decided to crack into
tolsun (the irc server Sun machine at Oulu), and naturally ;-) got in
through a new hole in sendmail. (At that time Jyrki was still the best
cracker I knew...)"*

Jarkko got some friends at the Helsinki and Tampere Universities to start
running IRC servers when his number of users increased.

Other universities soon followed. Markku J&auml;rvinen helped improving
the client. At this time Jarkko realized that the rest of the BBS features
probably wouldn't fit in his program!

Jarkko got in touch with guys at the University of Denver and Oregon State
University. They had got an IRC network running (they had got the program
from one of Jarkko's friends, Vijay Subramaniam -- the first non-finnish
person to use IRC) and wanted to connect to the finnish network.

IRC then grew larger and got used on the entire Finnish national network -
Funet - and then connected to Nordunet, the Scandinavian branch of the
Internet.

In November 1988, IRC had spread across the Internet.

In the middle of 1989, there were some 40 servers worldwide. 

ircII was released 1989 by Michael Sandrof.

In July 1990, IRC averaged at 12 users on 38 servers.

In 1990, a new network was set up in order to develop a new version (2.6) of
the ircd. The network named ChNet (about 25 servers and no users) existed a
few months before disagreements among the programmers caused it to dissolve.

## EFnet

In August 1990 the first major disagreement took place in the IRC
world. The "A-net" (Anarchy net) included as server named
eris.berkeley.edu.  It was all open, required no passwords and had no
limit on the number of connects. As Greg "wumpus" Lindahl explains: "it
had a wildcard server line, so people were hooking up servers and
nick-colliding everyone".

The "Eris Free network", EFnet, made the eris machine the first to be
Q-lined (Q for quarantine) from IRC (wumpus' words again: "Eris refused
to remove that line, so I formed EFnet. It wasn't much of a fight; I got
all the hubs to join, and almost everyone else got carried
along."). A-net was formed with the eris servers, EFnet was formed with
the non-eris servers. History showed most servers and users went with
EFnet. The name EFnet lived only shortly, as soon as ANet had died, the
name EFnet became void too. There was one and only "IRC" left again for
a while.

TubNet was the next network to splinter off. It was created by a crowd of
people in #hottub that grew tired of all the netsplits. It got 5 servers
and around 100 users. It died again in September the same year.

One often-talked-about event in the history of IRC is the gulf war. In
early 1991, [live reports](
http://sunsite.unc.edu/pub/academic/communications/logs/Gulf-War/) were
available and more than 300 concurrent users were experienced for the
first time.

## Undernet

Another fork effort, the first that really made a big and lasting
difference, was initiated by 'Wildthang' in USA October 1992 (it forked
off the EFnet ircd version 2.8.10). It was meant to be just a test
network to develop bots on but it quickly grew to a network "for friends
and their friends". In Europe and Canada a separate new network was
being worked on (by '_dl' and 'WIZZARD') and in December the french
servers connected to the canadian ones, and in the end of the month, the
.fr-.ca network was connected to the US one and the network that later
came to be called "The Undernet" was born.

The "undernetters" wanted to take ircd further in an attempt to make it
less bandwidth consumptive and to try to sort out the channel chaos
(netsplits and takeovers) that EFnet started to suffer from. For the
latter purpose, the Undernet implemented timestamps, new routing and
offered the CService -- a program that allowed users to register
channels and then attempted to protect them from troublemakers. (More or
less a global defense bot.) The very first server list presented, from
Febrary 15th 1993, includes servers from USA, Canada, France, Kroatia
and Japan. On August 15th, the new user count record was set to 57
users.

## RFC 1459

In May 1993, the Request For Comments 1459, for the IRC protocol is out
for the public. It has since been subject to many violations and
extensions.

It is notable that the CTCP parts and things like colors and formats are
not included in the protocol spec. Nor is character encoding.

## Dalnet

During the summer (some sources mention July) 1994, the Undernet is
itself forked. This time, the new Network is called Dalnet (named after
its founder: dalvenjah), and they formed the new network for better user
service and even more user and channel protections. One of the more
significant changes in Dalnet already from the beginning is their use of
longer nicknames (the original ircd limit being 9 letters). Dalnet ircd
modifications were made by Alexei "Lefler" Kosut.

Dalnet was thus based on the undernet ircd server, although the dalnet
pioneers were EFnet abandoners. According to James Ng the initial dalnet
people were *"ops in #StarTrek sick from the constant
splits/lags/takeovers/etc"*.
  
Dalnet quickly offered global WallOps (IRCop messages that can be seen by
users who are +w (/mode NickName +w)), longer nicknames, Q:Lined nicknames
(nicknames that cannot be used i.e.  ChanServ, IRCop, NickServ, etc.),
global K:Lines (ban of one person or an entire domain from a server or the
entire network), IRCop only communications: GlobOps, +H mode showing that
an IRCop is a "helpop" etc.

Much of Dalnet's new functions were written in early 1995 by Brian
"Morpher" Smith and allow users to own nicknames, channels, send memos
and more.

## oz.org

Undernet split (again) in March 1996 when the sole Australian server
delinked from Undernet because of difficulties with the connection
across the TransPacific Australian/United States network link. The first
few months of oz.org's existance were primarily a trial delink from the
Undernet because of the inability to maintain a link during peak usage
hours. One of the two designers (chaos and seks) of the orginal Undernet
X and W chanserv was Australian, and the same code was used for Oz.org's
Z (the name of the chanserv). In June 2001, ozorg boasted peak usages of
4,000 simultaneous users.

## IRCnet

In July 1996, after months of flame wars and discussions on the mailing
list, there was yet another split due to disagreement in how the
development of the ircd should evolve. Most notably, the "european"
(most of those servers were in europe) side that later named itself
IRCnet argued for nick and channel delays, where the EFnet side argued
for timestamps. Most (not all) of the IRCnet servers were in Europe,
while most of the EFnet server were in the US. This event is also known
as "The Great Split" in many IRC societies. EFnet has since (as of
August 1998) grown and passed the number of users it had then. In the
autumn year 2000, EFnet has some 50,000 users and IRCnet 70,000.

## Freenode - Open Projects Network

Yet another IRC network that opened its doors in 1998 named the Open
Projects Network, and had about 100 users and less than 20 channels that
year. In late 2001 it had grown to nearly 4,000 users and over 1,300
channels. The OPN uses the Dancer IRCD server, after having been using ircu
the intial few years.

This network was later renamed to <b>Freenode</b>.

In 2011, it peaks at 65,000 users in 40,000 channels.

## libera.chat

In May 2021, there's a mass admin exodus from Freenode (after
disagreements with the owner of parts of the infra) and many of the
admins instead set camp over in the recently created [libera.chat](
https://libera.chat">libera.chat) network. Many channels formerly on
Freenode follows on over to libera.

## Other Networks

Of course, while internet is booming so does IRC. There exists hundreds
of independent IRC networks today (like amiganet, linuxnet, galaxynet,
bestnet, NewNet, AnotherNet, ChatNet, UpperNet, ZAnet, X-Net, GammaNet,
SuperChat, IceNet, RedBrasil, GR-Net, AlphaStar, SorceryNet etc), but
luckily there is "only" four of the main ones (this was the reality back
in 1998) that keep develop their own version of the ircd server
software.

Of course, as of 2002, lots of other networks have popped up and now
numerous of them are developing their own customized versions of the IRC
protocol.

## Further Standardization Attempts

IETF-IRCUP was an initiative started in January 1998, to gather all the
flavours of IRC servers to document a new RFC and possibly set a new
standard for all networks to commit to. That project died.

CTCP/2 was an attempt, started in 1997 by Bjorn Reese, to develop and
standardize the Client To Client Protocol that was never in the
RFC. Clients have been known to extend and modify the original CTCP
protocol without allowing non-compliant clients to filter the new
codes. CTCP/2 was meant to define how codes and perhaps more important
new codes should be introduced in order to let old clients remain
functional. It was also meant to address the IPv6 problems the DCC
intiating sequence has. The CTCP/2 project died as well.

[IRCv3](https://ircv3.net/) - *"We’re the IRCv3 Working Group – a
collection of IRC software developers and network staff that develop
extensions to the IRC client protocol"*
  
We'll just have to wait and see what the future of IRC has to show...

## IRC Popularity

 According to measurements done by [irc.netsplit.de](
https://irc.netsplit.de/networks/top10.php), IRC in general have lost
users gradually ever since 2004/2005. Those years, the top 4 IRC
networks all had over 100,000 users each on a daily basis. Those
networks were Quakenet, Undernet, IRCnet and EFnet. Quakenet was in the
lead with more than 200,000 users.

In the beginning of 2011, Quakenet is just above 100,000 users and the
only network over 100K.

In 2021, Freenode (before its demise) is the largest one with peak of
90,000 users in Febrary.

## Thanks to

I did not experience all of this. I found information on various places
and I received information from various people in order to write
this. People that have helped me with this include:

 - Greg "wumpus" Lindahl
 - Vesa "vesa" Ruokonen
 - James Ng
 - Tuomas Heino
 - Richard (eagle`s on undernet)
 - Ari Lemmke
