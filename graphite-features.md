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
to the equivalent [OpenType feature](opentype-features.md).

The following list includes the features with an OpenType equivalent.
[Further down](#nonotf) is a list of those Graphite features that do not have an
OpenType analogue.

- locl serb Serbian-style alternates
- cv43 Engs 1024 Uppercase Eng alternates
 - `0` Large eng with descender
 - `1` Large eng on baseline
 - `2` Capital N with tail
 - `3` Large eng with short stem
- cv75 viet 1029 Vietnamese-style diacritics 
- ss01 litr 1032 Literacy alternates
- cv68 Y_hk 1034 Capital Y-hook alternates
- cv44 N_hk 1035 Capital N-left-hook alternate
- cv70 apos 1044 Modifier apostrophe alternates
- cv71 coln 1047 Modifier colon alternate
- cv46 opnO 1059 Open-O alternate
- cv25 ramh 1025 Rams horn alternates
 - 0 Small bowl
 - 1 Large bowl
 - 2 Small gamma
- cv91 tone 1026 Tone numbers
- cv80 mone 1027 Mongolian-style Cyrillic E
- cv82 sbrv 1028 Combining breve Cyrillic form
- ss06 invs 1030 Show invisible characters
- ss04 bowl 1031 Barred-bowl forms
- cv62 v_hk 1033 V-hook alternates
 - 0 Curved
 - 1 Straight with low hook
 - 2 Straight with high hook
- cv19 ezhc 1036 Small ezh-curl alternate
- cv57 t_hk 1037 Capital T-hook alternate
- cv28 Hstk 1038 Capital H-stroke alternate
- cv55 R_tl 1039 Capital R-tail alternate
- cv49 p_hk 1040 Small p-hook alternate
- cv20 Ezhr 1042 Capital Ezh alternates
- cv76 ogon 1043 Ogonek alternate
- cv47 opOU 1045 OU alternates
- cv98 empt 1046 Empty set alternates
- cv37 Jstk 1049 J-stroke hook alternate
- cv92 tstv 1050 Hide contour staves
- ss05 ital 1053 Slant italic specials
- cv81 shha 1056 Cyrillic shha alternate
- cv90 chtn 1057 Chinantec toens
- smcp,c2sc smcp 1058 Small caps
- cv77 cam 1063 Non-European caron alternates
- cv13 B_hk 1064 Capital B-hook alternate
- cv13 D-hk Capital D-hook alternate
- cv10 dig0 1065 Digit zero with slash
- cv01 dig1 1066 Digit one without base
- cv04 dig4 1067 Digit four with open top
- cv06 dg69 1068 Digit six and nine alternates
- cv07 dig7 1069 Digit seven with bar
- cv31 i_tl 1070 Small i-tail alternate
- cv34 jser 1071 Small j-serif alternate
- cv39 l_tl 1072 Small l-tail alternate
- cv51 q_tl 1073 Small q-tail alternate
- `cv56` `t_tl` 1074 Small t-tail alternate 
- cv67 y_tl 1075 Small y-tail alternate
- cv52 Qalt 1076 Capital Q alternate


<a name="nonotf"></a>

Graphite features currently without an OpenType feature equivalent
------------------------------------------------------------------

- brig 1052 Bridging diacritics 
- pit9 1062 9-level pitches
 - 0 No tramlines
 - 1 Tramlines
 - 2 Non-ligated with no tramlines
 - 3 Non-ligated with tramlines

- 1048 Orthographic glottal alternate *deprecated*
- beta 1060 Serif beta alternate *deprecated*
- dpua 1077 Show deprecated PUA *deprecated*
- dsel 1051 Diacritic selection *deprecated*
- lopr 1054 Low-profile diacritics *deprecated*
- romn 1041 Romanian-style diacritics *deprecated*
