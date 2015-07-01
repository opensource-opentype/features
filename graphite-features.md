Graphite features
=================

Unlike OpenType and AAT, Graphites advanced font-feature support does
not stem from a pre-defined list of possible features.  Instead, font
developers can define and name features in any manner they wish.

This does constitute a bit of a practical challenge for application
developers, but because the Graphite-enabled fonts most likely to be
encountered are those from SIL, any potential for confusion can be
averted by taking a look at the Graphite features SIL implements.

SIL maintains a [list of feature
definitions](http://scripts.sil.org/SILUnicodeRF_Features) on its site
that covers the feature set used by the Andika, Charis, Doulos, and
Gentium font familes.

Originally, SIL's font families used numeric IDs to identify each
feature.  As of the 5.000 releases in 2014, however, the features all
use four-character alphabetic IDs, many of which correspond directly
to the equivalent [OpenType feature](otf-features.md).

The following list includes the features with an OpenType equivalent;
the corresponding OpenType feature tag is listed in italics.  The old,
numeric IDs for the Graphite features are in parentheses.
[Further down](#nonotf) is a list of those Graphite features that do not have an
OpenType analogue.

- `apos`	*cv70*	(formerly `1044`) Modifier apostrophe alternates
- `B_hk`	*cv13*	(formerly `1064`) Capital B-hook alternate
- `bowl`	*ss04*	(formerly `1031`) Barred-bowl forms
- `brig`		(formerly `1052`) Bridging diacritics
- `carn`	*cv77*	(formerly `1063`) Non-European caron alternates
- `chtn`	*cv90*	(formerly `1057`) Chinantec toens
- `coln`	*cv71*	(formerly `1047`) Modifier colon alternate
- `dg69`	*cv06*	(formerly `1068`) Digit six and nine alternates
- `D_hk`	*cv17*	Capital D-hook alternate
- `dig0`	*cv10*	(formerly `1065`) Digit zero with slash
- `dig1`	*cv01*	(formerly `1066`) Digit one without base
- `dig4`	*cv04*	(formerly `1067`) Digit four with open top
- `dig7`	*cv07*	(formerly `1069`) Digit seven with bar
- `empt`	*cv98*	(formerly `1046`) Empty set alternates
- `Engs`	*cv43*	(formerly `1024`) Uppercase Eng alternates
 - `0` Large eng with descender
 - `1` Large eng on baseline
 - `2` Capital N with tail
 - `3` Large eng with short stem
- `ezhc`	*cv19*	(formerly `1036`) Small ezh-curl alternate
- `Ezhr`	*cv20*	(formerly `1042`) Capital Ezh alternates
- `Hstk`	*cv28*	(formerly `1038`) Capital H-stroke alternate
- `invs`	*ss06*	(formerly `1030`) Show invisible characters
- `ital`	*ss05*	(formerly `1053`) Slant italic specials
- `i_tl`	*cv31*	(formerly `1070`) Small i-tail alternate
- `jser`	*cv34*	(formerly `1071`) Small j-serif alternate
- `Jstk`	*cv37*	(formerly `1049`) J-stroke hook alternate
- `litr`	*ss01*	(formerly `1032`) Literacy alternates
- `l_tl`	*cv39*	(formerly `1072`) Small l-tail alternate
- `mone`	*cv80*	(formerly `1027`) Mongolian-style Cyrillic E
- `N_hk`	*cv44*	(formerly `1035`) Capital N-left-hook alternate
- `ogon`	*cv76*	(formerly `1043`) Ogonek alternate
- `opnO`	*cv46*	(formerly `1059`) Open-O alternate
- `opOU`	*cv47*	(formerly `1045`) OU alternates
- `p_hk`	*cv49*	(formerly `1040`) Small p-hook alternate
- `pit9`		(formerly `1062`) 9-level pitches
- `Qalt`	*cv52*	(formerly `1076`) Capital Q alternate
- `q_tl`	*cv51*	(formerly `1073`) Small q-tail alternate
- `ramh`	*cv25*	(formerly `1025`) Rams horn alternates
 - `0` Small bowl
 - `1` Large bowl
 - `2` Small gamma
- `R_tl`	*cv55*	(formerly `1039`) Capital R-tail alternate
- `sbrv`	*cv82*	(formerly `1028`) Combining breve Cyrillic form
- `serb`	*locl*	Serbian-style alternates
- `shha`	*cv81*	(formerly `1056`) Cyrillic shha alternate
- `smcp`	*smcp,c2sc*	(formerly `1058`) Small caps
- `t_hk`	*cv57*	(formerly `1037`) Capital T-hook alternate
- `tone`	*cv91*	(formerly `1026`) Tone numbers
- `tstv`	*cv92*	(formerly `1050, formerly`) Hide contour staves
- `t_tl`	*cv56*	(formerly `1074`) Small t-tail alternate
- `v_hk`	*cv62*	(formerly `1033`) V-hook alternates
 - `0` Curved
 - `1` Straight with low hook
 - `2` Straight with high hook
- `viet`	*cv75*	(formerly `1029`) Vietnamese-style diacritics
- `Y_hk`	*cv68*	(formerly `1034`) Capital Y-hook alternates
- `y_tl`	*cv67*	(formerly `1075`) Small y-tail alternate

<a name="nonotf"></a>

Graphite features currently `without an OpenType feature equivalent
------------------------------------------------------------------

- `brig`		(formerly `1052`) Bridging diacritics 
- `pit9`		(formerly `1062`) 9-level pitches
 - `0`	No tramlines
 - `1`	Tramlines
 - `2`	Non-ligated with no tramlines
 - `3`	Non-ligated with tramlines

- `1048`		Orthographic glottal alternate *deprecated*
- `beta`		(formerly `1060`) Serif beta alternate *deprecated*
- `dpua`		(formerly `1077`) Show deprecated PUA *deprecated*
- `dsel`		(formerly `1051`) Diacritic selection *deprecated*
- `lopr`		(formerly `1054`) Low-profile diacritics *deprecated*
- `romn`		(formerly `1041`) Romanian-style diacritics *deprecated*
