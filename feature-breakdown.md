A breakdown of advanced font feature implementation issues
==========================================================

The [OpenType](otf-features.md), [AAT](aat-features.md), and [Graphite](graphite-features.md) font features present 3 implementation
questions for application developers:

- Which features should be enabled by default if they are present in the font
- Which features should be activated automatically by context
- Which features should be explicitly presented to the user in the user interface

Defaults
--------

Adobe, Microsoft, and FontLab's Adam Twardoch each have a set of
recommendations as to which features ought to be activated by
default.  They are indicated in green in the following table.

The three lists agree on *most* features; those where there are
conflicts are discussed below in the [conflicts](#conflicts) section.

<table cellspacing="0" border="0">
	<colgroup width="64"></colgroup>
	<colgroup width="293"></colgroup>
	<colgroup span="3" width="129"></colgroup>
	<colgroup width="89"></colgroup>
	<tr>
		<td height="17" align="left" valign=bottom><i><font color="#000000">Tag</font></i></td>
		<td align="left" valign=bottom><i><font color="#000000">Feature</font></i></td>
		<td align="left" valign=bottom><i><font color="#000000">Default: Adobe</font></i></td>
		<td align="left" valign=bottom><i><font color="#000000">Default: MS</font></i></td>
		<td align="left" valign=bottom><i><font color="#000000">Default: Twardoch</font></i></td>
		<td align="left" valign=bottom><i><font color="#000000">UI: Trawdoch</font></i></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">aalt</font></td>
		<td align="left" valign=bottom><font color="#000000">Access All Alternates</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000">special</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">abvf</font></td>
		<td align="left" valign=bottom><font color="#000000">Above-base Forms</font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">abvm</font></td>
		<td align="left" valign=bottom><font color="#000000">Above-base Mark Positioning</font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">abvs</font></td>
		<td align="left" valign=bottom><font color="#000000">Above-base Substitutions</font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">afrc</font></td>
		<td align="left" valign=bottom><font color="#000000">Alternative Fractions</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000">yes</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">akhn</font></td>
		<td align="left" valign=bottom><font color="#000000">Akhands</font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">altv</font></td>
		<td align="left" valign=bottom><font color="#000000">Alternate Vertical Metrics [deprecated]</font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">blwf</font></td>
		<td align="left" valign=bottom><font color="#000000">Below-base Forms</font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">blwm</font></td>
		<td align="left" valign=bottom><font color="#000000">Below-base Mark Positioning</font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">blws</font></td>
		<td align="left" valign=bottom><font color="#000000">Below-base Substitutions</font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">calt</font></td>
		<td align="left" valign=bottom><font color="#000000">Contextual Alternates</font></td>
		<td align="left" valign=bottom bgcolor="#6AD46A"><font color="#000000">on</font></td>
		<td align="left" valign=bottom bgcolor="#6AD46A"><font color="#000000">on</font></td>
		<td align="left" valign=bottom bgcolor="#6AD46A"><font color="#000000">on</font></td>
		<td align="left" valign=bottom><font color="#000000">yes</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">case</font></td>
		<td align="left" valign=bottom><font color="#000000">Case-Sensitive Forms</font></td>
		<td align="left" valign=bottom bgcolor="#FBA743"><font color="#000000">contextual</font></td>
		<td align="left" valign=bottom bgcolor="#FBA743"><font color="#000000">contextual</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000">yes</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">ccmp</font></td>
		<td align="left" valign=bottom><font color="#000000">Glyph Composition / Decomposition</font></td>
		<td align="left" valign=bottom bgcolor="#6AD46A"><font color="#000000">on</font></td>
		<td align="left" valign=bottom bgcolor="#6AD46A"><font color="#000000">on</font></td>
		<td align="left" valign=bottom bgcolor="#6AD46A"><font color="#000000">on</font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">cfar</font></td>
		<td align="left" valign=bottom><font color="#000000">Conjunct Form After Ro</font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">cjct</font></td>
		<td align="left" valign=bottom><font color="#000000">Conjunct Forms</font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">clig</font></td>
		<td align="left" valign=bottom><font color="#000000">Contextual Ligatures</font></td>
		<td align="left" valign=bottom bgcolor="#6AD46A"><font color="#000000">on</font></td>
		<td align="left" valign=bottom bgcolor="#6AD46A"><font color="#000000">on</font></td>
		<td align="left" valign=bottom bgcolor="#6AD46A"><font color="#000000">on</font></td>
		<td align="left" valign=bottom><font color="#000000">yes</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">cpct</font></td>
		<td align="left" valign=bottom><font color="#000000">Centered CJK Punctuation</font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">cpsp</font></td>
		<td align="left" valign=bottom><font color="#000000">Capital Spacing</font></td>
		<td align="left" valign=bottom bgcolor="#6AD46A"><font color="#000000">on</font></td>
		<td align="left" valign=bottom bgcolor="#6AD46A"><font color="#000000">on</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000">yes</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">crcy</font></td>
		<td align="left" valign=bottom><font color="#000000">Currency [deprecated]</font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">cswh</font></td>
		<td align="left" valign=bottom><font color="#000000">Contextual Swash</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000">yes</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">curs</font></td>
		<td align="left" valign=bottom><font color="#000000">Cursive Positioning</font></td>
		<td align="left" valign=bottom bgcolor="#62C4D7"><font color="#000000">user</font></td>
		<td align="left" valign=bottom bgcolor="#62C4D7"><font color="#000000">user</font></td>
		<td align="left" valign=bottom bgcolor="#6AD46A"><font color="#000000">on</font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">cv01-99</font></td>
		<td align="left" valign=bottom><font color="#000000">Character Variants</font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000">yes</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">c2pc</font></td>
		<td align="left" valign=bottom><font color="#000000">Petite Capitals From Capitals</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000">yes</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">c2sc</font></td>
		<td align="left" valign=bottom><font color="#000000">Small Capitals From Capitals</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000">yes</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">dflt</font></td>
		<td align="left" valign=bottom><font color="#000000">Default processing [deprecated]</font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">dist</font></td>
		<td align="left" valign=bottom><font color="#000000">Distances</font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">dlig</font></td>
		<td align="left" valign=bottom><font color="#000000">Discretionary Ligatures</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000">yes</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">dnom</font></td>
		<td align="left" valign=bottom><font color="#000000">Denominators</font></td>
		<td align="left" valign=bottom bgcolor="#CC99FF"><font color="#000000">dependent</font></td>
		<td align="left" valign=bottom bgcolor="#CC99FF"><font color="#000000">dependent</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000">yes</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">dpng</font></td>
		<td align="left" valign=bottom><font color="#000000">Dipthongs [deprecated]</font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
		<td align="left" valign=bottom bgcolor="#C0C0C0"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">dtls</font></td>
		<td align="left" valign=bottom><font color="#000000">Dotless forms</font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
		<td align="left" valign=bottom bgcolor="#CC99FF"><font color="#000000">dependent</font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">expt</font></td>
		<td align="left" valign=bottom><font color="#000000">Expert Forms</font></td>
		<td align="left" valign=bottom bgcolor="#62C4D7"><font color="#000000">user</font></td>
		<td align="left" valign=bottom bgcolor="#62C4D7"><font color="#000000">user</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000">yes</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">falt</font></td>
		<td align="left" valign=bottom><font color="#000000">Final Glyph on Line Alternates</font></td>
		<td align="left" valign=bottom bgcolor="#62C4D7"><font color="#000000">user</font></td>
		<td align="left" valign=bottom bgcolor="#62C4D7"><font color="#000000">user</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000">yes</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">fin2</font></td>
		<td align="left" valign=bottom><font color="#000000">Terminal Forms #2</font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">fin3</font></td>
		<td align="left" valign=bottom><font color="#000000">Terminal Forms #3</font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">fina</font></td>
		<td align="left" valign=bottom><font color="#000000">Terminal Forms</font></td>
		<td align="left" valign=bottom bgcolor="#6AD46A"><font color="#000000">on</font></td>
		<td align="left" valign=bottom bgcolor="#6AD46A"><font color="#000000">on</font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom><font color="#000000">special</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">flac</font></td>
		<td align="left" valign=bottom><font color="#000000">Flattened Ascent Forms</font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
		<td align="left" valign=bottom bgcolor="#FBA743"><font color="#000000">contextual</font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">frac</font></td>
		<td align="left" valign=bottom><font color="#000000">Fractions</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000">yes</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">fwid</font></td>
		<td align="left" valign=bottom><font color="#000000">Full Widths</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000">yes</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">half</font></td>
		<td align="left" valign=bottom><font color="#000000">Half Forms</font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">haln</font></td>
		<td align="left" valign=bottom><font color="#000000">Halant Forms</font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">halt</font></td>
		<td align="left" valign=bottom><font color="#000000">Alternate Half Widths</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000">yes</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">hist</font></td>
		<td align="left" valign=bottom><font color="#000000">Historical Forms</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000">yes</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">hkna</font></td>
		<td align="left" valign=bottom><font color="#000000">Horizontal Kana Alternates</font></td>
		<td align="left" valign=bottom><font color="#000000">of</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#FBA743"><font color="#000000">contextual</font></td>
		<td align="left" valign=bottom><font color="#000000">special</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">hlig</font></td>
		<td align="left" valign=bottom><font color="#000000">Historical Ligatures</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000">yes</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">hngl</font></td>
		<td align="left" valign=bottom><font color="#000000">Hangul</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000">yes</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">hojo</font></td>
		<td align="left" valign=bottom><font color="#000000">Hojo Kanji Forms (JIS X 0212-1990 Kanji Forms)</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000">yes</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">hwid</font></td>
		<td align="left" valign=bottom><font color="#000000">Half Widths</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000">yes</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">init</font></td>
		<td align="left" valign=bottom><font color="#000000">Initial Forms</font></td>
		<td align="left" valign=bottom bgcolor="#6AD46A"><font color="#000000">on</font></td>
		<td align="left" valign=bottom bgcolor="#6AD46A"><font color="#000000">on</font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom><font color="#000000">special</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">isol</font></td>
		<td align="left" valign=bottom><font color="#000000">Isolated Forms</font></td>
		<td align="left" valign=bottom bgcolor="#6AD46A"><font color="#000000">on</font></td>
		<td align="left" valign=bottom bgcolor="#6AD46A"><font color="#000000">on</font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom><font color="#000000">special</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">ital</font></td>
		<td align="left" valign=bottom><font color="#000000">Italics</font></td>
		<td align="left" valign=bottom bgcolor="#9752B9"><font color="#000000">integrated</font></td>
		<td align="left" valign=bottom bgcolor="#9752B9"><font color="#000000">integrated</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000">yes</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">jajp</font></td>
		<td align="left" valign=bottom><font color="#000000">Japanese Forms [deprecated]</font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">jalt</font></td>
		<td align="left" valign=bottom><font color="#000000">Justification Alternates</font></td>
		<td align="left" valign=bottom bgcolor="#62C4D7"><font color="#000000">user</font></td>
		<td align="left" valign=bottom bgcolor="#62C4D7"><font color="#000000">user</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000">yes</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">jp78</font></td>
		<td align="left" valign=bottom><font color="#000000">JIS78 Forms</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000">yes</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">jp83</font></td>
		<td align="left" valign=bottom><font color="#000000">JIS83 Forms</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000">yes</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">jp90</font></td>
		<td align="left" valign=bottom><font color="#000000">JIS90 Forms</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000">yes</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">jp03</font></td>
		<td align="left" valign=bottom><font color="#000000">JIS03 Forms [deprecated]</font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">jp04</font></td>
		<td align="left" valign=bottom><font color="#000000">JIS2004 Forms</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000">yes</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">kern</font></td>
		<td align="left" valign=bottom><font color="#000000">Kerning</font></td>
		<td align="left" valign=bottom bgcolor="#6AD46A"><font color="#000000">on</font></td>
		<td align="left" valign=bottom bgcolor="#6AD46A"><font color="#000000">on</font></td>
		<td align="left" valign=bottom bgcolor="#6AD46A"><font color="#000000">on</font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">kokr</font></td>
		<td align="left" valign=bottom><font color="#000000">Korean Forms [deprecated]</font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">lfbd</font></td>
		<td align="left" valign=bottom><font color="#000000">Left Bounds</font></td>
		<td align="left" valign=bottom bgcolor="#CC99FF"><font color="#000000">dependent</font></td>
		<td align="left" valign=bottom bgcolor="#CC99FF"><font color="#000000">dependent</font></td>
		<td align="left" valign=bottom bgcolor="#6AD46A"><font color="#000000">on</font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">liga</font></td>
		<td align="left" valign=bottom><font color="#000000">Standard Ligatures</font></td>
		<td align="left" valign=bottom bgcolor="#6AD46A"><font color="#000000">on</font></td>
		<td align="left" valign=bottom bgcolor="#6AD46A"><font color="#000000">on</font></td>
		<td align="left" valign=bottom bgcolor="#6AD46A"><font color="#000000">on</font></td>
		<td align="left" valign=bottom><font color="#000000">yes</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">ljmo</font></td>
		<td align="left" valign=bottom><font color="#000000">Leading Jamo Forms</font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">lnum</font></td>
		<td align="left" valign=bottom><font color="#000000">Lining Figures</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000">yes</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">locl</font></td>
		<td align="left" valign=bottom><font color="#000000">Localized Forms</font></td>
		<td align="left" valign=bottom bgcolor="#6AD46A"><font color="#000000">on</font></td>
		<td align="left" valign=bottom bgcolor="#6AD46A"><font color="#000000">on</font></td>
		<td align="left" valign=bottom bgcolor="#6AD46A"><font color="#000000">on</font></td>
		<td align="left" valign=bottom><font color="#000000">special</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">ltra</font></td>
		<td align="left" valign=bottom><font color="#000000">Left-to-right alternates</font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
		<td align="left" valign=bottom bgcolor="#C0C0C0"><font color="#000000">?</font></td>
		<td align="left" valign=bottom><font color="#000000">bidi</font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">ltrm</font></td>
		<td align="left" valign=bottom><font color="#000000">Left-to-right mirrored forms</font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
		<td align="left" valign=bottom bgcolor="#C0C0C0"><font color="#000000">?</font></td>
		<td align="left" valign=bottom><font color="#000000">bidi</font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">mark</font></td>
		<td align="left" valign=bottom><font color="#000000">Mark Positioning</font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom bgcolor="#6AD46A"><font color="#000000">on</font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">med2</font></td>
		<td align="left" valign=bottom><font color="#000000">Medial Forms #2</font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom bgcolor="#6AD46A"><font color="#000000">on</font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">medi</font></td>
		<td align="left" valign=bottom><font color="#000000">Medial Forms</font></td>
		<td align="left" valign=bottom bgcolor="#6AD46A"><font color="#000000">on</font></td>
		<td align="left" valign=bottom bgcolor="#6AD46A"><font color="#000000">on</font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom><font color="#000000">special</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">mgrk</font></td>
		<td align="left" valign=bottom><font color="#000000">Mathematical Greek</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000">yes</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">mkmk</font></td>
		<td align="left" valign=bottom><font color="#000000">Mark to Mark Positioning</font></td>
		<td align="left" valign=bottom bgcolor="#6AD46A"><font color="#000000">on</font></td>
		<td align="left" valign=bottom bgcolor="#6AD46A"><font color="#000000">on</font></td>
		<td align="left" valign=bottom bgcolor="#6AD46A"><font color="#000000">on</font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">mset</font></td>
		<td align="left" valign=bottom><font color="#000000">Mark Positioning via Substitution</font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom bgcolor="#6AD46A"><font color="#000000">on</font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">nalt</font></td>
		<td align="left" valign=bottom><font color="#000000">Alternate Annotation Forms</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000">yes</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">nlck</font></td>
		<td align="left" valign=bottom><font color="#000000">NLC Kanji Forms</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000">yes</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">nukt</font></td>
		<td align="left" valign=bottom><font color="#000000">Nukta Forms</font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">numr</font></td>
		<td align="left" valign=bottom><font color="#000000">Numerators</font></td>
		<td align="left" valign=bottom bgcolor="#CC99FF"><font color="#000000">dependent</font></td>
		<td align="left" valign=bottom bgcolor="#CC99FF"><font color="#000000">dependent</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000">yes</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">onum</font></td>
		<td align="left" valign=bottom><font color="#000000">Oldstyle Figures</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000">yes</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">opbd</font></td>
		<td align="left" valign=bottom><font color="#000000">Optical Bounds</font></td>
		<td align="left" valign=bottom bgcolor="#6AD46A"><font color="#000000">on</font></td>
		<td align="left" valign=bottom bgcolor="#6AD46A"><font color="#000000">on</font></td>
		<td align="left" valign=bottom bgcolor="#6AD46A"><font color="#000000">on</font></td>
		<td align="left" valign=bottom><font color="#000000">special</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">ordn</font></td>
		<td align="left" valign=bottom><font color="#000000">Ordinals</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000">yes</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">ornm</font></td>
		<td align="left" valign=bottom><font color="#000000">Ornaments</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000">yes</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">palt</font></td>
		<td align="left" valign=bottom><font color="#000000">Proportional Alternate Widths</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000">yes</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">pcap</font></td>
		<td align="left" valign=bottom><font color="#000000">Petite Capitals</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000">yes</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">pkna</font></td>
		<td align="left" valign=bottom><font color="#000000">Proportional Kana</font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000">yes</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">pnum</font></td>
		<td align="left" valign=bottom><font color="#000000">Proportional Figures</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000">yes</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">pref</font></td>
		<td align="left" valign=bottom><font color="#000000">Pre-Base Forms</font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">pres</font></td>
		<td align="left" valign=bottom><font color="#000000">Pre-base Substitutions</font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">pstf</font></td>
		<td align="left" valign=bottom><font color="#000000">Post-base Forms</font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">psts</font></td>
		<td align="left" valign=bottom><font color="#000000">Post-base Substitutions</font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">pwid</font></td>
		<td align="left" valign=bottom><font color="#000000">Proportional Widths</font></td>
		<td align="left" valign=bottom bgcolor="#62C4D7"><font color="#000000">user</font></td>
		<td align="left" valign=bottom bgcolor="#62C4D7"><font color="#000000">user</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000">yes</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">qwid</font></td>
		<td align="left" valign=bottom><font color="#000000">Quarter Widths</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000">yes</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">rand</font></td>
		<td align="left" valign=bottom><font color="#000000">Randomize</font></td>
		<td align="left" valign=bottom bgcolor="#62C4D7"><font color="#000000">user / on</font></td>
		<td align="left" valign=bottom bgcolor="#62C4D7"><font color="#000000">user / on</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000">yes</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">rclt</font></td>
		<td align="left" valign=bottom><font color="#000000">Required Contextual Alternates</font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
		<td align="left" valign=bottom bgcolor="#6AD46A"><font color="#000000">on</font></td>
		<td align="left" valign=bottom bgcolor="#6AD46A"><font color="#000000">on</font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">rkrf</font></td>
		<td align="left" valign=bottom><font color="#000000">Rakar Forms</font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">rlig</font></td>
		<td align="left" valign=bottom><font color="#000000">Required Ligatures</font></td>
		<td align="left" valign=bottom bgcolor="#6AD46A"><font color="#000000">on</font></td>
		<td align="left" valign=bottom bgcolor="#6AD46A"><font color="#000000">on</font></td>
		<td align="left" valign=bottom bgcolor="#6AD46A"><font color="#000000">on</font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">rphf</font></td>
		<td align="left" valign=bottom><font color="#000000">Reph Forms</font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">rtbd</font></td>
		<td align="left" valign=bottom><font color="#000000">Right Bounds</font></td>
		<td align="left" valign=bottom bgcolor="#CC99FF"><font color="#000000">dependent</font></td>
		<td align="left" valign=bottom bgcolor="#CC99FF"><font color="#000000">dependent</font></td>
		<td align="left" valign=bottom bgcolor="#6AD46A"><font color="#000000">on</font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">rtla</font></td>
		<td align="left" valign=bottom><font color="#000000">Right-to-left alternates</font></td>
		<td align="left" valign=bottom bgcolor="#C0C0C0"><font color="#000000">?</font></td>
		<td align="left" valign=bottom bgcolor="#C0C0C0"><font color="#000000">?</font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">rtlm</font></td>
		<td align="left" valign=bottom><font color="#000000">Right-to-left mirrored forms</font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
		<td align="left" valign=bottom bgcolor="#C0C0C0"><font color="#000000">?</font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">ruby</font></td>
		<td align="left" valign=bottom><font color="#000000">Ruby Notation Forms</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000">yes</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">salt</font></td>
		<td align="left" valign=bottom><font color="#000000">Stylistic Alternates</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000">yes</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">sinf</font></td>
		<td align="left" valign=bottom><font color="#000000">Scientific Inferiors</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000">yes</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">size</font></td>
		<td align="left" valign=bottom><font color="#000000">Optical size</font></td>
		<td align="left" valign=bottom bgcolor="#6AD46A"><font color="#000000">on</font></td>
		<td align="left" valign=bottom bgcolor="#6AD46A"><font color="#000000">on</font></td>
		<td align="left" valign=bottom bgcolor="#6AD46A"><font color="#000000">on</font></td>
		<td align="left" valign=bottom><font color="#000000">special</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">smcp</font></td>
		<td align="left" valign=bottom><font color="#000000">Small Capitals</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000">yes</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">smpl</font></td>
		<td align="left" valign=bottom><font color="#000000">Simplified Forms</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000">yes</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">ss01-20</font></td>
		<td align="left" valign=bottom><font color="#000000">Stylistic Sets 1 to 20</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000">yes</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">ssty</font></td>
		<td align="left" valign=bottom><font color="#000000">Math Script Style Alternates</font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
		<td align="left" valign=bottom bgcolor="#CC99FF"><font color="#000000">dependent</font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">stch</font></td>
		<td align="left" valign=bottom><font color="#000000">Stretching Glyph Decomposition</font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
		<td align="left" valign=bottom bgcolor="#6AD46A"><font color="#000000">on</font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">subs</font></td>
		<td align="left" valign=bottom><font color="#000000">Subscript</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000">yes</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">sups</font></td>
		<td align="left" valign=bottom><font color="#000000">Superscript</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000">yes</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">swsh</font></td>
		<td align="left" valign=bottom><font color="#000000">Swash</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000">yes</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">titl</font></td>
		<td align="left" valign=bottom><font color="#000000">Titling</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000">yes</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">tjmo</font></td>
		<td align="left" valign=bottom><font color="#000000">Trailing Jamo Forms</font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">tnam</font></td>
		<td align="left" valign=bottom><font color="#000000">Traditional Name Forms</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000">yes</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">tnum</font></td>
		<td align="left" valign=bottom><font color="#000000">Tabular Figures</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000">yes</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">trad</font></td>
		<td align="left" valign=bottom><font color="#000000">Traditional Forms</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000">yes</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">twid</font></td>
		<td align="left" valign=bottom><font color="#000000">Third Widths</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000">yes</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">unic</font></td>
		<td align="left" valign=bottom><font color="#000000">Unicase</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000">yes</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">valt</font></td>
		<td align="left" valign=bottom><font color="#000000">Alternate Vertical Metrics</font></td>
		<td align="left" valign=bottom bgcolor="#FBA743"><font color="#000000">contextual</font></td>
		<td align="left" valign=bottom bgcolor="#FBA743"><font color="#000000">contextual</font></td>
		<td align="left" valign=bottom bgcolor="#FBA743"><font color="#000000">contextual</font></td>
		<td align="left" valign=bottom><font color="#000000">special</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">vatu</font></td>
		<td align="left" valign=bottom><font color="#000000">Vattu Variants</font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">vert</font></td>
		<td align="left" valign=bottom><font color="#000000">Vertical Writing</font></td>
		<td align="left" valign=bottom bgcolor="#FBA743"><font color="#000000">contextual</font></td>
		<td align="left" valign=bottom bgcolor="#FBA743"><font color="#000000">contextual</font></td>
		<td align="left" valign=bottom bgcolor="#FBA743"><font color="#000000">contextual</font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">vhal</font></td>
		<td align="left" valign=bottom><font color="#000000">Alternate Vertical Half Metrics</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000">yes</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">vivn</font></td>
		<td align="left" valign=bottom><font color="#000000">Vietnamese Forms [deprecated]</font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">vjmo</font></td>
		<td align="left" valign=bottom><font color="#000000">Vowel Jamo Forms</font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom bgcolor="#FFE763"><font color="#000000"><em>complex shaper</em></font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">vkna</font></td>
		<td align="left" valign=bottom><font color="#000000">Vertical Kana Alternates</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#FBA743"><font color="#000000">contextual</font></td>
		<td align="left" valign=bottom><font color="#000000">special</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">vkrn</font></td>
		<td align="left" valign=bottom><font color="#000000">Vertical Kerning</font></td>
		<td align="left" valign=bottom bgcolor="#FBA743"><font color="#000000">contextual</font></td>
		<td align="left" valign=bottom bgcolor="#FBA743"><font color="#000000">contextual</font></td>
		<td align="left" valign=bottom bgcolor="#FBA743"><font color="#000000">contextual</font></td>
		<td align="left" valign=bottom><font color="#000000">special</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">vpal</font></td>
		<td align="left" valign=bottom><font color="#000000">Proportional Alternate Vertical Metrics</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000">yes</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">vrt2</font></td>
		<td align="left" valign=bottom><font color="#000000">Vertical Alternates and Rotation</font></td>
		<td align="left" valign=bottom bgcolor="#FBA743"><font color="#000000">contextual</font></td>
		<td align="left" valign=bottom bgcolor="#FBA743"><font color="#000000">contextual</font></td>
		<td align="left" valign=bottom bgcolor="#FBA743"><font color="#000000">contextual</font></td>
		<td align="left" valign=bottom><font color="#000000">special</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">zero</font></td>
		<td align="left" valign=bottom><font color="#000000">Slashed Zero</font></td>
		<td align="left" valign=bottom bgcolor="#62C4D7"><font color="#000000">user</font></td>
		<td align="left" valign=bottom bgcolor="#62C4D7"><font color="#000000">user</font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000">yes</font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">zhcn</font></td>
		<td align="left" valign=bottom><font color="#000000">Simplified Chinese Forms [deprecated]</font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
	</tr>
	<tr>
		<td height="17" align="left" valign=bottom><font color="#000000">zntw</font></td>
		<td align="left" valign=bottom><font color="#000000">Traditional Chinese Forms [deprecated]</font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
		<td align="left" valign=bottom bgcolor="#E94F5D"><font color="#000000">off</font></td>
		<td align="left" valign=bottom><font color="#000000"><br></font></td>
	</tr>
</table>

<a name="conflicts"></a>

Conflicts between recommendations
---------------------------------

There are 22 features where the various specification recommendations
disagree about the correct default state, *not* counting those
instances where one or more of the documents is silent on the question.

altv 	Alternate Vertical Metrics [deprecated]
case 	Case-Sensitive Forms
curs 	Cursive Positioning
expt 	Expert Forms
falt 	Final Glyph on Line Alternates
fina 	Terminal Forms
hkna 	Horizontal Kana Alternates
init 	Initial Forms
isol 	Isolated Forms
ital 	Italics
jalt 	Justification Alternates
lfbd 	Left Bounds
mark 	Mark Positioning
med2 	Medial Forms #2
medi 	Medial Forms
mset 	Mark Positioning via Substitution
pwid 	Proportional Widths
rand 	Randomize
rtbd 	Right Bounds
ssty 	Math Script Style Alternates
zero 	Slashed Zero

Several others Twardoch recommends off-by-default or leaving the
decision up to the shaper, while Adode and Microsoft say the feature
should be automatically enabled by context, since it is dependent on
another feature:

dnom 	Denominators
dtls 	Dotless forms
numr 	Numerators


<a name="ui"></a>

UI exposure
-----------

Twardoch makes a point of highlighting those features which should be
accessible through the user interface.


