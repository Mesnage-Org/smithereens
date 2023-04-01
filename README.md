# Fraph

## EBNF Notation for PG Structures (https://github.com/matthijsgroen/ebnf2railroad)
```
(*
  The PG Structural Language
  ==========================
*)

Multimer = Monomer , { ( "~" (* Glycosidic Bond *) | Crosslink ) , Monomer } ;

Crosslink
  = "=" (* Ambiguous Crosslink *)
  | ( "=" , digit , ( "<" | ">" ) , digit , "=" ,
    { ":" , "=" , digit , ( "<" | ">" ) , digit , "=" } )
  ;

Monomer = Glycan , [ "-" , Peptide ] ;

Glycan = Monosaccharide , [ Modifications ] ,
  { Monosaccharide , [ Modifications ] } ;

Peptide = AminoAcid , [ Modifications ] ,
  [ LateralChain ] , { AminoAcid , [ Modifications ] ,
  [ LateralChain ] } ;

LateralChain = "[" , Peptide , "]" ;

Monosaccharide = lowercase ;

AminoAcid = uppercase ;

Modifications = "(" , ( "+" | "-" ) , Moiety ,
  { "," , { space } , ( "+" | "-" ) , Moiety } , ")" ;

Moiety = letter , { letter | digit | "_" } ;

(*
  Basic components
  ----------------
  These are low level components, the small building blocks.
*)

space = " " | "\t" ;

letter = uppercase | lowercase ;

uppercase
  = "A" | "B" | "C" | "D" | "E" | "F" | "G"
  | "H" | "I" | "J" | "K" | "L" | "M" | "N"
  | "O" | "P" | "Q" | "R" | "S" | "T" | "U"
  | "V" | "W" | "X" | "Y" | "Z"
  ;

lowercase
  = "a" | "b" | "c" | "d" | "e" | "f" | "g"
  | "h" | "i" | "j" | "k" | "l" | "m" | "n"
  | "o" | "p" | "q" | "r" | "s" | "t" | "u"
  | "v" | "w" | "x" | "y" | "z"
  ;

digit
  = "0" | "1" | "2" | "3" | "4" | "5" | "6"
  | "7" | "8" | "9"
  ;
```