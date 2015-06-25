Feature mappings in HarfBuzz
============================

The font features described by [OpenType](otf-features.md), [AAT](aat-features.md), and [Graphite](graphite-features.md) are not
indentical.  However, in many cases there is a clear mapping between 
them.

The OpenType shaping library HarfBuzz supports a
[mapping](https://github.com/behdad/harfbuzz/blob/master/src/hb-coretext.cc#L341)
between AAT and OpenType features that covers most, but not all of the
AAT codes.

The first thing to note is that the AAT codes tend to be more
granular.  So, for example, the `c2sc` OpenType feature, which means
"captials to small caps," maps to a set of two AAT selectors taken
together: `kUpperCaseSmallCapsSelector` + `kDefaultUpperCaseSelector`.

The other thing to note is that there are several AAT codes not
currently supported in this mapping.  Excluding deprecated code and
the codes that are exlcusively tied to script-shaping features, they are:

- `kRequiredLigaturesOnSelector`	Required Ligatures
- `kRebusPicturesOnSelector`	Rebus Pictures
- `kDiphthongLigaturesOnSelector`	Diphthong Ligatures
- `kSquaredLigaturesOnSelector`	Squared Ligatures
- `kAbbrevSquaredLigaturesOnSelector`	Squared Ligatures, Abbreviated
- `kSymbolLigaturesOnSelector`	Symbol Ligatures
- `kWordInitialSwashesOnSelector`	Word Initial Swashes
- `kWordFinalSwashesOnSelector`	Word Final Swashes
- `kShowDiacriticsSelector`	Show Diacritics
- `kHideDiacriticsSelector`	Hide Diacritics
- `kDecomposeDiacriticsSelector`	Decompose Diacritics
- `kVerticalFractionsSelector`	Vertical Fractions
- `kNoOrnamentsSelector`	None
- `kDingbatsSelector`	Dingbats
- `kPiCharactersSelector`	Pi Characters
- `kFleuronsSelector`	Fleurons
- `kDecorativeBordersSelector`	Decorative Borders
- `kInternationalSymbolsSelector`	International Symbols
- `kMathSymbolsSelector`	Math Symbols
- `kCharacterAlternatives`	Character Alternatives
- `kDesignLevel1Selector`	Design Level 1
- `kDesignLevel2Selector`	Design Level 2
- `kDesignLevel3Selector`	Design Level 3
- `kDesignLevel4Selector`	Design Level 4
- `kDesignLevel5Selector`	Design Level 5
- `kDisplayTextSelector`	Display Text
- `kEngravedTextSelector`	Engraved Text
- `kIlluminatedCapsSelector`	Illuminated Caps
- `kTallCapsSelector`	Tall Caps
- `kNoAnnotationSelector`	No Annotation
- `kBoxAnnotationSelector`	Box Annotation
- `kRoundedBoxAnnotationSelector`	Rounded Box Annotation
- `kCircleAnnotationSelector`	Circle Annotation
- `kInvertedCircleAnnotationSelector`	Inverted Circle Annotation
- `kParenthesisAnnotationSelector`	Parenthesis Annotation
- `kPeriodAnnotationSelector`	Period Annotation
- `kRomanNumeralAnnotationSelector`	Roman Numeral Annotation
- `kDiamondAnnotationSelector`	Diamond Annotation
- `kInvertedBoxAnnotationSelector`	Inverted Box Annotation	
- `kInvertedRoundedBoxAnnotationSelector`	Inverted Rounded Box Annotation
