GREP(1)                          User Commands                         GREP(1)

NAME
       grep, egrep, fgrep, rgrep - print lines that match patterns

SYNOPSIS
       grep [OPTION...] PATTERNS [FILE...]
       grep [OPTION...] -e PATTERNS ... [FILE...]
       grep [OPTION...] -f PATTERN_FILE ... [FILE...]

DESCRIPTION
       grep  searches  for  PATTERNS  in  each  FILE.  PATTERNS is one or more
       patterns separated by newline characters, and  grep  prints  each  line
       that  matches a pattern.  Typically PATTERNS should be quoted when grep
       is used in a shell command.

       A FILE of “-”  stands  for  standard  input.   If  no  FILE  is  given,
       recursive  searches  examine  the  working  directory, and nonrecursive
       searches read standard input.

       In addition, the variant programs egrep, fgrep and rgrep are  the  same
       as  grep -E,  grep -F,  and  grep -r, respectively.  These variants are
       deprecated, but are provided for backward compatibility.

OPTIONS
   Generic Program Information
       --help Output a usage message and exit.

       -V, --version
              Output the version number of grep and exit.

   Pattern Syntax
       -E, --extended-regexp
              Interpret PATTERNS as extended regular  expressions  (EREs,  see
              below).

       -F, --fixed-strings
              Interpret PATTERNS as fixed strings, not regular expressions.

       -G, --basic-regexp
              Interpret  PATTERNS  as  basic  regular  expressions  (BREs, see
              below).  This is the default.

       -P, --perl-regexp
              Interpret  PATTERNS  as  Perl-compatible   regular   expressions
              (PCREs).   This option is experimental when combined with the -z
              (--null-data) option, and grep  -P  may  warn  of  unimplemented
              features.

   Matching Control
       -e PATTERNS, --regexp=PATTERNS
              Use  PATTERNS  as the patterns.  If this option is used multiple
              times or is combined with the -f (--file) option, search for all
              patterns  given.   This  option can be used to protect a pattern
              beginning with “-”.

       -f FILE, --file=FILE
              Obtain patterns from FILE, one per line.  If this option is used
              multiple  times  or  is  combined with the -e (--regexp) option,
              search for all patterns given.  The  empty  file  contains  zero
              patterns, and therefore matches nothing.

       -i, --ignore-case
              Ignore  case  distinctions  in  patterns and input data, so that
              characters that differ only in case match each other.

       --no-ignore-case
              Do not ignore case distinctions  in  patterns  and  input  data.
              This is the default.  This option is useful for passing to shell
              scripts that already use -i, to cancel its effects  because  the
              two options override each other.

       -v, --invert-match
              Invert the sense of matching, to select non-matching lines.

       -w, --word-regexp
              Select  only  those  lines  containing  matches  that form whole
              words.  The test is that the matching substring must  either  be
              at  the  beginning  of  the  line,  or  preceded  by  a non-word
              constituent character.  Similarly, it must be either at the  end
              of  the  line  or  followed by a non-word constituent character.
              Word-constituent  characters  are  letters,  digits,   and   the
              underscore.  This option has no effect if -x is also specified.

       -x, --line-regexp
              Select  only  those  matches  that exactly match the whole line.
              For a regular expression pattern, this  is  like  parenthesizing
              the pattern and then surrounding it with ^ and $.

       -y     Obsolete synonym for -i.

   General Output Control
       -c, --count
              Suppress  normal output; instead print a count of matching lines
              for each input file.  With the -v,  --invert-match  option  (see
              below), count non-matching lines.

       --color[=WHEN], --colour[=WHEN]
              Surround   the  matched  (non-empty)  strings,  matching  lines,
              context lines, file  names,  line  numbers,  byte  offsets,  and
              separators  (for fields and groups of context lines) with escape
              sequences to display them in color on the terminal.  The  colors
              are  defined  by  the  environment  variable  GREP_COLORS.   The
              deprecated environment variable GREP_COLOR is  still  supported,
              but  its setting does not have priority.  WHEN is never, always,
              or auto.

       -L, --files-without-match
              Suppress normal output; instead print the  name  of  each  input
              file from which no output would normally have been printed.  The
              scanning will stop on the first match.

       -l, --files-with-matches
              Suppress normal output; instead print the  name  of  each  input
              file  from  which  output would normally have been printed.  The
              scanning will stop on the first match.

       -m NUM, --max-count=NUM
              Stop reading a file after NUM matching lines.  If the  input  is
              standard  input  from a regular file, and NUM matching lines are
              output, grep ensures that the standard input  is  positioned  to
              just  after the last matching line before exiting, regardless of
              the presence of trailing context lines.  This enables a  calling
              process  to resume a search.  When grep stops after NUM matching
              lines, it outputs any trailing context lines.  When  the  -c  or
              --count  option  is  also  used,  grep  does  not output a count
              greater than NUM.  When the -v or --invert-match option is  also
              used, grep stops after outputting NUM non-matching lines.

       -o, --only-matching
              Print  only  the  matched  (non-empty) parts of a matching line,
              with each such part on a separate output line.

       -q, --quiet, --silent
              Quiet;  do  not  write  anything  to  standard   output.    Exit
              immediately  with  zero status if any match is found, even if an
              error was detected.  Also see the -s or --no-messages option.

       -s, --no-messages
              Suppress error messages about nonexistent or unreadable files.

   Output Line Prefix Control
       -b, --byte-offset
              Print the 0-based byte offset within the input file before  each
              line of output.  If -o (--only-matching) is specified, print the
              offset of the matching part itself.

       -H, --with-filename
              Print the file name for each match.  This is  the  default  when
              there is more than one file to search.

       -h, --no-filename
              Suppress  the  prefixing  of  file names on output.  This is the
              default when there is only one file (or only standard input)  to
              search.

       --label=LABEL
              Display  input  actually  coming  from  standard  input as input
              coming from file LABEL.  This can be useful  for  commands  that
              transform  a  file's  contents  before searching, e.g., gzip -cd
              foo.gz | grep --label=foo -H 'some pattern'.  See  also  the  -H
              option.

       -n, --line-number
              Prefix  each  line of output with the 1-based line number within
              its input file.

       -T, --initial-tab
              Make sure that the first character of actual line  content  lies
              on a tab stop, so that the alignment of tabs looks normal.  This
              is useful with options that prefix their output  to  the  actual
              content:  -H,-n,  and  -b.   In order to improve the probability
              that lines from a single file will all start at the same column,
              this also causes the line number and byte offset (if present) to
              be printed in a minimum size field width.

       -u, --unix-byte-offsets
              Report Unix-style byte offsets.   This  switch  causes  grep  to
              report  byte offsets as if the file were a Unix-style text file,
              i.e., with  CR  characters  stripped  off.   This  will  produce
              results  identical  to  running  grep  on  a Unix machine.  This
              option has no effect unless -b option is also used;  it  has  no
              effect on platforms other than MS-DOS and MS-Windows.

       -Z, --null
              Output  a  zero  byte  (the  ASCII NUL character) instead of the
              character that normally follows a file name.  For example,  grep
              -lZ  outputs  a  zero  byte  after each file name instead of the
              usual newline.  This option makes the output  unambiguous,  even
              in the presence of file names containing unusual characters like
              newlines.  This option can  be  used  with  commands  like  find
              -print0,  perl  -0,  sort  -z, and xargs -0 to process arbitrary
              file names, even those that contain newline characters.

   Context Line Control
       -A NUM, --after-context=NUM
              Print NUM  lines  of  trailing  context  after  matching  lines.
              Places   a  line  containing  a  group  separator  (--)  between
              contiguous groups of matches.  With the  -o  or  --only-matching
              option, this has no effect and a warning is given.

       -B NUM, --before-context=NUM
              Print  NUM  lines  of  leading  context  before  matching lines.
              Places  a  line  containing  a  group  separator  (--)   between
              contiguous  groups  of  matches.  With the -o or --only-matching
              option, this has no effect and a warning is given.

       -C NUM, -NUM, --context=NUM
              Print NUM lines of output context.  Places a line  containing  a
              group separator (--) between contiguous groups of matches.  With
              the -o or --only-matching option,  this  has  no  effect  and  a
              warning is given.

   File and Directory Selection
       -a, --text
              Process  a binary file as if it were text; this is equivalent to
              the --binary-files=text option.

       --binary-files=TYPE
              If a file's data or metadata indicate  that  the  file  contains
              binary  data,  assume  that  the file is of type TYPE.  Non-text
              bytes indicate binary data; these are either output  bytes  that
              are  improperly  encoded  for  the current locale, or null input
              bytes when the -z option is not given.

              By default, TYPE is binary, and  grep  suppresses  output  after
              null  input  binary  data  is  discovered, and suppresses output
              lines that contain improperly encoded data.  When some output is
              suppressed,  grep  follows  any  output  with a one-line message
              saying that a binary file matches.

              If TYPE is without-match, when grep discovers null input  binary
              data  it  assumes that the rest of the file does not match; this
              is equivalent to the -I option.

              If TYPE is text, grep processes a binary  file  as  if  it  were
              text; this is equivalent to the -a option.

              When  type  is  binary,  grep  may  treat non-text bytes as line
              terminators even without the -z  option.   This  means  choosing
              binary  versus text can affect whether a pattern matches a file.
              For example, when type is binary the pattern q$  might  match  q
              immediately  followed  by  a  null byte, even though this is not
              matched when type is text.  Conversely, when type is binary  the
              pattern . (period) might not match a null byte.

              Warning:  The  -a  option might output binary garbage, which can
              have nasty side effects if the output is a terminal and  if  the
              terminal driver interprets some of it as commands.  On the other
              hand, when reading files whose text encodings  are  unknown,  it
              can   be  helpful  to  use  -a  or  to  set  LC_ALL='C'  in  the
              environment, in order to find more matches even if  the  matches
              are unsafe for direct display.

       -D ACTION, --devices=ACTION
              If  an  input  file  is  a device, FIFO or socket, use ACTION to
              process it.  By  default,  ACTION  is  read,  which  means  that
              devices are read just as if they were ordinary files.  If ACTION
              is skip, devices are silently skipped.

       -d ACTION, --directories=ACTION
              If an input file is a directory, use ACTION to process  it.   By
              default,  ACTION is read, i.e., read directories just as if they
              were  ordinary  files.   If  ACTION  is  skip,   silently   skip
              directories.   If  ACTION  is recurse, read all files under each
              directory, recursively, following symbolic links  only  if  they
              are on the command line.  This is equivalent to the -r option.

       --exclude=GLOB
              Skip  any  command-line file with a name suffix that matches the
              pattern GLOB, using wildcard matching; a name suffix  is  either
              the  whole name, or a trailing part that starts with a non-slash
              character immediately after a  slash  (/)  in  the  name.   When
              searching  recursively, skip any subfile whose base name matches
              GLOB; the base name is the part after the last slash.  A pattern
              can  use *, ?, and [...] as wildcards, and \ to quote a wildcard
              or backslash character literally.

       --exclude-from=FILE
              Skip files whose base name matches any of  the  file-name  globs
              read  from  FILE  (using  wildcard  matching  as described under
              --exclude).

       --exclude-dir=GLOB
              Skip any command-line directory with a name suffix that  matches
              the   pattern   GLOB.   When  searching  recursively,  skip  any
              subdirectory whose base name matches GLOB.  Ignore any redundant
              trailing slashes in GLOB.

       -I     Process  a  binary  file as if it did not contain matching data;
              this is equivalent to the --binary-files=without-match option.

       --include=GLOB
              Search only files whose base name matches GLOB  (using  wildcard
              matching as described under --exclude).

       -r, --recursive
              Read  all  files  under  each  directory, recursively, following
              symbolic links only if they are on the command line.  Note  that
              if   no  file  operand  is  given,  grep  searches  the  working
              directory.  This is equivalent to the -d recurse option.

       -R, --dereference-recursive
              Read all files under each directory,  recursively.   Follow  all
              symbolic links, unlike -r.

   Other Options
       --line-buffered
              Use  line  buffering  on  output.   This can cause a performance
              penalty.

       -U, --binary
              Treat the file(s) as binary.  By default, under MS-DOS  and  MS-
              Windows,  grep  guesses  whether  a  file  is  text or binary as
              described for the --binary-files option.  If  grep  decides  the
              file  is  a  text  file,  it  strips  the CR characters from the
              original file contents (to make regular expressions with ^ and $
              work   correctly).   Specifying  -U  overrules  this  guesswork,
              causing all  files  to  be  read  and  passed  to  the  matching
              mechanism  verbatim; if the file is a text file with CR/LF pairs
              at  the  end  of  each  line,  this  will  cause  some   regular
              expressions  to  fail.   This  option has no effect on platforms
              other than MS-DOS and MS-Windows.

       -z, --null-data
              Treat  input  and  output  data  as  sequences  of  lines,  each
              terminated by a zero byte (the ASCII NUL character) instead of a
              newline.  Like the -Z or --null option, this option can be  used
              with commands like sort -z to process arbitrary file names.

REGULAR EXPRESSIONS
       A  regular  expression  is  a  pattern that describes a set of strings.
       Regular  expressions  are   constructed   analogously   to   arithmetic
       expressions, by using various operators to combine smaller expressions.

       grep understands three different versions of regular expression syntax:
       “basic” (BRE), “extended” (ERE) and “perl” (PCRE).  In GNU  grep  there
       is  no difference in available functionality between basic and extended
       syntaxes.  In other implementations, basic regular expressions are less
       powerful.   The  following  description  applies  to  extended  regular
       expressions; differences for basic regular expressions  are  summarized
       afterwards.    Perl-compatible   regular  expressions  give  additional
       functionality, and are documented in pcresyntax(3) and  pcrepattern(3),
       but work only if PCRE is available in the system.

       The  fundamental building blocks are the regular expressions that match
       a single character.  Most characters, including all letters and digits,
       are regular expressions that match themselves.  Any meta-character with
       special meaning may be quoted by preceding it with a backslash.

       The period . matches any single character.  It is  unspecified  whether
       it matches an encoding error.

   Character Classes and Bracket Expressions
       A  bracket  expression is a list of characters enclosed by [ and ].  It
       matches any single character in that list.  If the first  character  of
       the  list is the caret ^ then it matches any character not in the list;
       it is unspecified whether it matches an encoding error.   For  example,
       the regular expression [0123456789] matches any single digit.

       Within  a  bracket  expression,  a  range  expression  consists  of two
       characters separated by a hyphen.  It matches any single character that
       sorts  between  the  two  characters,  inclusive,  using  the  locale's
       collating sequence and character set.  For example, in  the  default  C
       locale, [a-d] is equivalent to [abcd].  Many locales sort characters in
       dictionary  order,  and  in  these  locales  [a-d]  is  typically   not
       equivalent to [abcd]; it might be equivalent to [aBbCcDd], for example.
       To obtain the traditional interpretation of  bracket  expressions,  you
       can  use the C locale by setting the LC_ALL environment variable to the
       value C.

       Finally, certain named classes  of  characters  are  predefined  within
       bracket expressions, as follows.  Their names are self explanatory, and
       they  are  [:alnum:],  [:alpha:],  [:blank:],   [:cntrl:],   [:digit:],
       [:graph:],  [:lower:],  [:print:], [:punct:], [:space:], [:upper:], and
       [:xdigit:].  For example, [[:alnum:]]  means  the  character  class  of
       numbers  and  letters in the current locale.  In the C locale and ASCII
       character set encoding, this is the same as  [0-9A-Za-z].   (Note  that
       the  brackets  in these class names are part of the symbolic names, and
       must be included in addition to the  brackets  delimiting  the  bracket
       expression.)   Most  meta-characters  lose their special meaning inside
       bracket expressions.  To include a literal ]  place  it  first  in  the
       list.   Similarly,  to include a literal ^ place it anywhere but first.
       Finally, to include a literal - place it last.

   Anchoring
       The caret ^ and the dollar sign $ are meta-characters that respectively
       match the empty string at the beginning and end of a line.

   The Backslash Character and Special Expressions
       The  symbols  \<  and  \>  respectively  match  the empty string at the
       beginning and end of a word.  The symbol \b matches the empty string at
       the  edge  of a word, and \B matches the empty string provided it's not
       at the edge of a word.  The symbol \w is a synonym for [_[:alnum:]] and
       \W is a synonym for [^_[:alnum:]].

   Repetition
       A  regular  expression  may  be  followed  by one of several repetition
       operators:
       ?      The preceding item is optional and matched at most once.
       *      The preceding item will be matched zero or more times.
       +      The preceding item will be matched one or more times.
       {n}    The preceding item is matched exactly n times.
       {n,}   The preceding item is matched n or more times.
       {,m}   The preceding item is matched at most m times.  This  is  a  GNU
              extension.
       {n,m}  The  preceding  item  is  matched at least n times, but not more
              than m times.

   Concatenation
       Two regular expressions may  be  concatenated;  the  resulting  regular
       expression  matches  any  string formed by concatenating two substrings
       that respectively match the concatenated expressions.

   Alternation
       Two regular expressions may be joined by  the  infix  operator  |;  the
       resulting   regular  expression  matches  any  string  matching  either
       alternate expression.

   Precedence
       Repetition takes precedence over concatenation,  which  in  turn  takes
       precedence  over  alternation.   A  whole expression may be enclosed in
       parentheses  to  override   these   precedence   rules   and   form   a
       subexpression.

   Back-references and Subexpressions
       The back-reference \n, where n is a single digit, matches the substring
       previously matched  by  the  nth  parenthesized  subexpression  of  the
       regular expression.

   Basic vs Extended Regular Expressions
       In  basic  regular expressions the meta-characters ?, +, {, |, (, and )
       lose their special meaning; instead use the  backslashed  versions  \?,
       \+, \{, \|, \(, and \).

EXIT STATUS
       Normally the exit status is 0 if a line is selected, 1 if no lines were
       selected, and 2 if an error occurred.  However, if the -q or --quiet or
       --silent  is  used and a line is selected, the exit status is 0 even if
       an error occurred.

ENVIRONMENT
       The  behavior  of  grep  is  affected  by  the  following   environment
       variables.

       The  locale  for  category  LC_foo  is specified by examining the three
       environment variables LC_ALL, LC_foo, LANG, in that order.   The  first
       of  these  variables that is set specifies the locale.  For example, if
       LC_ALL is not set, but LC_MESSAGES is set to pt_BR, then the  Brazilian
       Portuguese  locale  is used for the LC_MESSAGES category.  The C locale
       is used if none of these environment variables are set, if  the  locale
       catalog  is  not  installed,  or if grep was not compiled with national
       language support (NLS).  The shell command locale -a lists locales that
       are currently available.

       GREP_OPTIONS
              This variable specifies default options to be placed in front of
              any explicit options.  As  this  causes  problems  when  writing
              portable  scripts,  this  feature  will  be  removed in a future
              release of grep, and grep warns if it is used.   Please  use  an
              alias or script instead.

       GREP_COLOR
              This  variable  specifies  the  color  used to highlight matched
              (non-empty) text.  It is deprecated in favor of GREP_COLORS, but
              still supported.  The mt, ms, and mc capabilities of GREP_COLORS
              have priority over it.  It can only specify the  color  used  to
              highlight  the  matching  non-empty text in any matching line (a
              selected line when the -v command-line option is omitted,  or  a
              context line when -v is specified).  The default is 01;31, which
              means a bold red  foreground  text  on  the  terminal's  default
              background.

       GREP_COLORS
              Specifies  the  colors  and  other  attributes used to highlight
              various parts of the output.  Its  value  is  a  colon-separated
              list       of       capabilities      that      defaults      to
              ms=01;31:mc=01;31:sl=:cx=:fn=35:ln=32:bn=32:se=36  with  the  rv
              and  ne  boolean  capabilities omitted (i.e., false).  Supported
              capabilities are as follows.

              sl=    SGR substring for whole selected  lines  (i.e.,  matching
                     lines when the -v command-line option is omitted, or non-
                     matching lines when -v is  specified).   If  however  the
                     boolean  rv capability and the -v command-line option are
                     both specified, it  applies  to  context  matching  lines
                     instead.   The  default  is  empty  (i.e., the terminal's
                     default color pair).

              cx=    SGR substring for whole context lines (i.e., non-matching
                     lines  when  the  -v  command-line  option is omitted, or
                     matching lines when -v is  specified).   If  however  the
                     boolean  rv capability and the -v command-line option are
                     both specified, it applies to selected non-matching lines
                     instead.   The  default  is  empty  (i.e., the terminal's
                     default color pair).

              rv     Boolean value that reverses (swaps) the meanings  of  the
                     sl=  and cx= capabilities when the -v command-line option
                     is specified.  The default is false (i.e., the capability
                     is omitted).

              mt=01;31
                     SGR substring for matching non-empty text in any matching
                     line (i.e., a selected  line  when  the  -v  command-line
                     option   is  omitted,  or  a  context  line  when  -v  is
                     specified).  Setting this is equivalent to  setting  both
                     ms=  and mc= at once to the same value.  The default is a
                     bold  red  text  foreground   over   the   current   line
                     background.

              ms=01;31
                     SGR  substring  for matching non-empty text in a selected
                     line.  (This is only used when the -v command-line option
                     is  omitted.)   The  effect  of  the  sl=  (or cx= if rv)
                     capability  remains  active  when  this  kicks  in.   The
                     default  is  a  bold red text foreground over the current
                     line background.

              mc=01;31
                     SGR substring for matching non-empty text  in  a  context
                     line.  (This is only used when the -v command-line option
                     is specified.)  The effect of the  cx=  (or  sl=  if  rv)
                     capability  remains  active  when  this  kicks  in.   The
                     default is a bold red text foreground  over  the  current
                     line background.

              fn=35  SGR  substring for file names prefixing any content line.
                     The  default  is  a  magenta  text  foreground  over  the
                     terminal's default background.

              ln=32  SGR  substring  for  line  numbers  prefixing any content
                     line.  The default is a green text  foreground  over  the
                     terminal's default background.

              bn=32  SGR  substring  for  byte  offsets  prefixing any content
                     line.  The default is a green text  foreground  over  the
                     terminal's default background.

              se=36  SGR  substring  for  separators that are inserted between
                     selected line fields (:), between  context  line  fields,
                     (-),  and  between  groups of adjacent lines when nonzero
                     context is specified (--).  The default is  a  cyan  text
                     foreground over the terminal's default background.

              ne     Boolean  value  that prevents clearing to the end of line
                     using Erase in Line (EL) to Right  (\33[K)  each  time  a
                     colorized  item  ends.   This  is  needed on terminals on
                     which EL is not supported.  It  is  otherwise  useful  on
                     terminals  for  which  the back_color_erase (bce) boolean
                     terminfo capability  does  not  apply,  when  the  chosen
                     highlight colors do not affect the background, or when EL
                     is too slow or causes too much flicker.  The  default  is
                     false (i.e., the capability is omitted).

              Note  that  boolean  capabilities  have  no =... part.  They are
              omitted (i.e., false) by default and become true when specified.

              See  the  Select  Graphic  Rendition  (SGR)   section   in   the
              documentation  of  the  text terminal that is used for permitted
              values  and  their  meaning  as  character  attributes.    These
              substring  values are integers in decimal representation and can
              be concatenated with semicolons.  grep takes care of  assembling
              the  result  into  a  complete  SGR sequence (\33[...m).  Common
              values to concatenate include 1 for bold, 4 for underline, 5 for
              blink,  7 for inverse, 39 for default foreground color, 30 to 37
              for foreground colors, 90 to 97  for  16-color  mode  foreground
              colors,  38;5;0  to  38;5;255  for  88-color and 256-color modes
              foreground colors, 49 for default background color, 40 to 47 for
              background  colors,  100  to  107  for  16-color mode background
              colors, and 48;5;0 to 48;5;255 for 88-color and 256-color  modes
              background colors.

       LC_ALL, LC_COLLATE, LANG
              These  variables specify the locale for the LC_COLLATE category,
              which determines the collating sequence used to interpret  range
              expressions like [a-z].

       LC_ALL, LC_CTYPE, LANG
              These  variables  specify  the locale for the LC_CTYPE category,
              which determines the type of characters, e.g., which  characters
              are  whitespace.   This  category  also determines the character
              encoding, that is, whether text is encoded in UTF-8,  ASCII,  or
              some  other  encoding.  In the C or POSIX locale, all characters
              are encoded  as  a  single  byte  and  every  byte  is  a  valid
              character.

       LC_ALL, LC_MESSAGES, LANG
              These variables specify the locale for the LC_MESSAGES category,
              which determines the language that grep uses for messages.   The
              default C locale uses American English messages.

       POSIXLY_CORRECT
              If  set, grep behaves as POSIX requires; otherwise, grep behaves
              more like other GNU programs.  POSIX requires that options  that
              follow  file  names  must  be treated as file names; by default,
              such options are permuted to the front of the operand  list  and
              are  treated as options.  Also, POSIX requires that unrecognized
              options be diagnosed as “illegal”, but since they are not really
              against  the  law  the default is to diagnose them as “invalid”.
              POSIXLY_CORRECT  also   disables   _N_GNU_nonoption_argv_flags_,
              described below.

       _N_GNU_nonoption_argv_flags_
              (Here  N is grep's numeric process ID.)  If the ith character of
              this environment variable's value is 1, do not consider the  ith
              operand  of  grep to be an option, even if it appears to be one.
              A shell can put  this  variable  in  the  environment  for  each
              command  it  runs,  specifying which operands are the results of
              file name wildcard expansion and therefore should not be treated
              as  options.   This  behavior  is  available only with the GNU C
              library, and only when POSIXLY_CORRECT is not set.

NOTES
       This man page is maintained only fitfully; the  full  documentation  is
       often more up-to-date.

COPYRIGHT
       Copyright 1998-2000, 2002, 2005-2020 Free Software Foundation, Inc.

       This is free software; see the source for copying conditions.  There is
       NO warranty; not even for MERCHANTABILITY or FITNESS FOR  A  PARTICULAR
       PURPOSE.

BUGS
   Reporting Bugs
       Email  bug reports to the bug-reporting address ⟨bug-grep@gnu.org⟩.  An
       email archive ⟨https://lists.gnu.org/mailman/listinfo/bug-grep⟩  and  a
       bug   tracker  ⟨https://debbugs.gnu.org/cgi/pkgreport.cgi?package=grep⟩
       are available.

   Known Bugs
       Large repetition counts in the {n,m} construct may cause  grep  to  use
       lots of memory.  In addition, certain other obscure regular expressions
       require exponential time and space, and may cause grep to  run  out  of
       memory.

       Back-references are very slow, and may require exponential time.

EXAMPLE
       The  following  example  outputs  the location and contents of any line
       containing “f” and ending in “.c”, within all files in the current  di‐
       rectory whose names contain “g” and end in “.h”.  The -n option outputs
       line numbers, the -- argument treats  expansions  of  “*g*.h”  starting
       with “-” as file names not options, and the empty file /dev/null causes
       file names to be output even if only one file name happens to be of the
       form “*g*.h”.

         $ grep -n -- 'f.*\.c$' *g*.h /dev/null
         argmatch.h:1:/* definitions and prototypes for argmatch.c

       The only line that matches is line 1 of argmatch.h.  Note that the reg‐
       ular expression syntax used in the pattern differs  from  the  globbing
       syntax that the shell uses to match file names.

SEE ALSO
   Regular Manual Pages
       awk(1),  cmp(1),  diff(1), find(1), perl(1), sed(1), sort(1), xargs(1),
       read(2), pcre(3), pcresyntax(3), pcrepattern(3), terminfo(5),  glob(7),
       regex(7).

   Full Documentation
       A complete manual ⟨https://www.gnu.org/software/grep/manual/⟩ is avail‐
       able.  If the info and grep programs are  properly  installed  at  your
       site, the command

              info grep

       should give you access to the complete manual.

GNU grep 3.4                      2019-12-29                           GREP(1)
GREP(1)                          User Commands                         GREP(1)

NAME
       grep, egrep, fgrep, rgrep - print lines that match patterns

SYNOPSIS
       grep [OPTION...] PATTERNS [FILE...]
       grep [OPTION...] -e PATTERNS ... [FILE...]
       grep [OPTION...] -f PATTERN_FILE ... [FILE...]

DESCRIPTION
       grep  searches  for  PATTERNS  in  each  FILE.  PATTERNS is one or more
       patterns separated by newline characters, and  grep  prints  each  line
       that  matches a pattern.  Typically PATTERNS should be quoted when grep
       is used in a shell command.

       A FILE of “-”  stands  for  standard  input.   If  no  FILE  is  given,
       recursive  searches  examine  the  working  directory, and nonrecursive
       searches read standard input.

       In addition, the variant programs egrep, fgrep and rgrep are  the  same
       as  grep -E,  grep -F,  and  grep -r, respectively.  These variants are
       deprecated, but are provided for backward compatibility.

OPTIONS
   Generic Program Information
       --help Output a usage message and exit.

       -V, --version
              Output the version number of grep and exit.

   Pattern Syntax
       -E, --extended-regexp
              Interpret PATTERNS as extended regular  expressions  (EREs,  see
              below).

       -F, --fixed-strings
              Interpret PATTERNS as fixed strings, not regular expressions.

       -G, --basic-regexp
              Interpret  PATTERNS  as  basic  regular  expressions  (BREs, see
              below).  This is the default.

       -P, --perl-regexp
              Interpret  PATTERNS  as  Perl-compatible   regular   expressions
              (PCREs).   This option is experimental when combined with the -z
              (--null-data) option, and grep  -P  may  warn  of  unimplemented
              features.

   Matching Control
       -e PATTERNS, --regexp=PATTERNS
              Use  PATTERNS  as the patterns.  If this option is used multiple
              times or is combined with the -f (--file) option, search for all
              patterns  given.   This  option can be used to protect a pattern
              beginning with “-”.

       -f FILE, --file=FILE
              Obtain patterns from FILE, one per line.  If this option is used
              multiple  times  or  is  combined with the -e (--regexp) option,
              search for all patterns given.  The  empty  file  contains  zero
              patterns, and therefore matches nothing.

       -i, --ignore-case
              Ignore  case  distinctions  in  patterns and input data, so that
              characters that differ only in case match each other.

       --no-ignore-case
              Do not ignore case distinctions  in  patterns  and  input  data.
              This is the default.  This option is useful for passing to shell
              scripts that already use -i, to cancel its effects  because  the
              two options override each other.

       -v, --invert-match
              Invert the sense of matching, to select non-matching lines.

       -w, --word-regexp
              Select  only  those  lines  containing  matches  that form whole
              words.  The test is that the matching substring must  either  be
              at  the  beginning  of  the  line,  or  preceded  by  a non-word
              constituent character.  Similarly, it must be either at the  end
              of  the  line  or  followed by a non-word constituent character.
              Word-constituent  characters  are  letters,  digits,   and   the
              underscore.  This option has no effect if -x is also specified.

       -x, --line-regexp
              Select  only  those  matches  that exactly match the whole line.
              For a regular expression pattern, this  is  like  parenthesizing
              the pattern and then surrounding it with ^ and $.

       -y     Obsolete synonym for -i.

   General Output Control
       -c, --count
              Suppress  normal output; instead print a count of matching lines
              for each input file.  With the -v,  --invert-match  option  (see
              below), count non-matching lines.

       --color[=WHEN], --colour[=WHEN]
              Surround   the  matched  (non-empty)  strings,  matching  lines,
              context lines, file  names,  line  numbers,  byte  offsets,  and
              separators  (for fields and groups of context lines) with escape
              sequences to display them in color on the terminal.  The  colors
              are  defined  by  the  environment  variable  GREP_COLORS.   The
              deprecated environment variable GREP_COLOR is  still  supported,
              but  its setting does not have priority.  WHEN is never, always,
              or auto.

       -L, --files-without-match
              Suppress normal output; instead print the  name  of  each  input
              file from which no output would normally have been printed.  The
              scanning will stop on the first match.

       -l, --files-with-matches
              Suppress normal output; instead print the  name  of  each  input
              file  from  which  output would normally have been printed.  The
              scanning will stop on the first match.

       -m NUM, --max-count=NUM
              Stop reading a file after NUM matching lines.  If the  input  is
              standard  input  from a regular file, and NUM matching lines are
              output, grep ensures that the standard input  is  positioned  to
              just  after the last matching line before exiting, regardless of
              the presence of trailing context lines.  This enables a  calling
              process  to resume a search.  When grep stops after NUM matching
              lines, it outputs any trailing context lines.  When  the  -c  or
              --count  option  is  also  used,  grep  does  not output a count
              greater than NUM.  When the -v or --invert-match option is  also
              used, grep stops after outputting NUM non-matching lines.

       -o, --only-matching
              Print  only  the  matched  (non-empty) parts of a matching line,
              with each such part on a separate output line.

       -q, --quiet, --silent
              Quiet;  do  not  write  anything  to  standard   output.    Exit
              immediately  with  zero status if any match is found, even if an
              error was detected.  Also see the -s or --no-messages option.

       -s, --no-messages
              Suppress error messages about nonexistent or unreadable files.

   Output Line Prefix Control
       -b, --byte-offset
              Print the 0-based byte offset within the input file before  each
              line of output.  If -o (--only-matching) is specified, print the
              offset of the matching part itself.

       -H, --with-filename
              Print the file name for each match.  This is  the  default  when
              there is more than one file to search.

       -h, --no-filename
              Suppress  the  prefixing  of  file names on output.  This is the
              default when there is only one file (or only standard input)  to
              search.

       --label=LABEL
              Display  input  actually  coming  from  standard  input as input
              coming from file LABEL.  This can be useful  for  commands  that
              transform  a  file's  contents  before searching, e.g., gzip -cd
              foo.gz | grep --label=foo -H 'some pattern'.  See  also  the  -H
              option.

       -n, --line-number
              Prefix  each  line of output with the 1-based line number within
              its input file.

       -T, --initial-tab
              Make sure that the first character of actual line  content  lies
              on a tab stop, so that the alignment of tabs looks normal.  This
              is useful with options that prefix their output  to  the  actual
              content:  -H,-n,  and  -b.   In order to improve the probability
              that lines from a single file will all start at the same column,
              this also causes the line number and byte offset (if present) to
              be printed in a minimum size field width.

       -u, --unix-byte-offsets
              Report Unix-style byte offsets.   This  switch  causes  grep  to
              report  byte offsets as if the file were a Unix-style text file,
              i.e., with  CR  characters  stripped  off.   This  will  produce
              results  identical  to  running  grep  on  a Unix machine.  This
              option has no effect unless -b option is also used;  it  has  no
              effect on platforms other than MS-DOS and MS-Windows.

       -Z, --null
              Output  a  zero  byte  (the  ASCII NUL character) instead of the
              character that normally follows a file name.  For example,  grep
              -lZ  outputs  a  zero  byte  after each file name instead of the
              usual newline.  This option makes the output  unambiguous,  even
              in the presence of file names containing unusual characters like
              newlines.  This option can  be  used  with  commands  like  find
              -print0,  perl  -0,  sort  -z, and xargs -0 to process arbitrary
              file names, even those that contain newline characters.

   Context Line Control
       -A NUM, --after-context=NUM
              Print NUM  lines  of  trailing  context  after  matching  lines.
              Places   a  line  containing  a  group  separator  (--)  between
              contiguous groups of matches.  With the  -o  or  --only-matching
              option, this has no effect and a warning is given.

       -B NUM, --before-context=NUM
              Print  NUM  lines  of  leading  context  before  matching lines.
              Places  a  line  containing  a  group  separator  (--)   between
              contiguous  groups  of  matches.  With the -o or --only-matching
              option, this has no effect and a warning is given.

       -C NUM, -NUM, --context=NUM
              Print NUM lines of output context.  Places a line  containing  a
              group separator (--) between contiguous groups of matches.  With
              the -o or --only-matching option,  this  has  no  effect  and  a
              warning is given.

   File and Directory Selection
       -a, --text
              Process  a binary file as if it were text; this is equivalent to
              the --binary-files=text option.

       --binary-files=TYPE
              If a file's data or metadata indicate  that  the  file  contains
              binary  data,  assume  that  the file is of type TYPE.  Non-text
              bytes indicate binary data; these are either output  bytes  that
              are  improperly  encoded  for  the current locale, or null input
              bytes when the -z option is not given.

              By default, TYPE is binary, and  grep  suppresses  output  after
              null  input  binary  data  is  discovered, and suppresses output
              lines that contain improperly encoded data.  When some output is
              suppressed,  grep  follows  any  output  with a one-line message
              saying that a binary file matches.

              If TYPE is without-match, when grep discovers null input  binary
              data  it  assumes that the rest of the file does not match; this
              is equivalent to the -I option.

              If TYPE is text, grep processes a binary  file  as  if  it  were
              text; this is equivalent to the -a option.

              When  type  is  binary,  grep  may  treat non-text bytes as line
              terminators even without the -z  option.   This  means  choosing
              binary  versus text can affect whether a pattern matches a file.
              For example, when type is binary the pattern q$  might  match  q
              immediately  followed  by  a  null byte, even though this is not
              matched when type is text.  Conversely, when type is binary  the
              pattern . (period) might not match a null byte.

              Warning:  The  -a  option might output binary garbage, which can
              have nasty side effects if the output is a terminal and  if  the
              terminal driver interprets some of it as commands.  On the other
              hand, when reading files whose text encodings  are  unknown,  it
              can   be  helpful  to  use  -a  or  to  set  LC_ALL='C'  in  the
              environment, in order to find more matches even if  the  matches
              are unsafe for direct display.

       -D ACTION, --devices=ACTION
              If  an  input  file  is  a device, FIFO or socket, use ACTION to
              process it.  By  default,  ACTION  is  read,  which  means  that
              devices are read just as if they were ordinary files.  If ACTION
              is skip, devices are silently skipped.

       -d ACTION, --directories=ACTION
              If an input file is a directory, use ACTION to process  it.   By
              default,  ACTION is read, i.e., read directories just as if they
              were  ordinary  files.   If  ACTION  is  skip,   silently   skip
              directories.   If  ACTION  is recurse, read all files under each
              directory, recursively, following symbolic links  only  if  they
              are on the command line.  This is equivalent to the -r option.

       --exclude=GLOB
              Skip  any  command-line file with a name suffix that matches the
              pattern GLOB, using wildcard matching; a name suffix  is  either
              the  whole name, or a trailing part that starts with a non-slash
              character immediately after a  slash  (/)  in  the  name.   When
              searching  recursively, skip any subfile whose base name matches
              GLOB; the base name is the part after the last slash.  A pattern
              can  use *, ?, and [...] as wildcards, and \ to quote a wildcard
              or backslash character literally.

       --exclude-from=FILE
              Skip files whose base name matches any of  the  file-name  globs
              read  from  FILE  (using  wildcard  matching  as described under
              --exclude).

       --exclude-dir=GLOB
              Skip any command-line directory with a name suffix that  matches
              the   pattern   GLOB.   When  searching  recursively,  skip  any
              subdirectory whose base name matches GLOB.  Ignore any redundant
              trailing slashes in GLOB.

       -I     Process  a  binary  file as if it did not contain matching data;
              this is equivalent to the --binary-files=without-match option.

       --include=GLOB
              Search only files whose base name matches GLOB  (using  wildcard
              matching as described under --exclude).

       -r, --recursive
              Read  all  files  under  each  directory, recursively, following
              symbolic links only if they are on the command line.  Note  that
              if   no  file  operand  is  given,  grep  searches  the  working
              directory.  This is equivalent to the -d recurse option.

       -R, --dereference-recursive
              Read all files under each directory,  recursively.   Follow  all
              symbolic links, unlike -r.

   Other Options
       --line-buffered
              Use  line  buffering  on  output.   This can cause a performance
              penalty.

       -U, --binary
              Treat the file(s) as binary.  By default, under MS-DOS  and  MS-
              Windows,  grep  guesses  whether  a  file  is  text or binary as
              described for the --binary-files option.  If  grep  decides  the
              file  is  a  text  file,  it  strips  the CR characters from the
              original file contents (to make regular expressions with ^ and $
              work   correctly).   Specifying  -U  overrules  this  guesswork,
              causing all  files  to  be  read  and  passed  to  the  matching
              mechanism  verbatim; if the file is a text file with CR/LF pairs
              at  the  end  of  each  line,  this  will  cause  some   regular
              expressions  to  fail.   This  option has no effect on platforms
              other than MS-DOS and MS-Windows.

       -z, --null-data
              Treat  input  and  output  data  as  sequences  of  lines,  each
              terminated by a zero byte (the ASCII NUL character) instead of a
              newline.  Like the -Z or --null option, this option can be  used
              with commands like sort -z to process arbitrary file names.

REGULAR EXPRESSIONS
       A  regular  expression  is  a  pattern that describes a set of strings.
       Regular  expressions  are   constructed   analogously   to   arithmetic
       expressions, by using various operators to combine smaller expressions.

       grep understands three different versions of regular expression syntax:
       “basic” (BRE), “extended” (ERE) and “perl” (PCRE).  In GNU  grep  there
       is  no difference in available functionality between basic and extended
       syntaxes.  In other implementations, basic regular expressions are less
       powerful.   The  following  description  applies  to  extended  regular
       expressions; differences for basic regular expressions  are  summarized
       afterwards.    Perl-compatible   regular  expressions  give  additional
       functionality, and are documented in pcresyntax(3) and  pcrepattern(3),
       but work only if PCRE is available in the system.

       The  fundamental building blocks are the regular expressions that match
       a single character.  Most characters, including all letters and digits,
       are regular expressions that match themselves.  Any meta-character with
       special meaning may be quoted by preceding it with a backslash.

       The period . matches any single character.  It is  unspecified  whether
       it matches an encoding error.

   Character Classes and Bracket Expressions
       A  bracket  expression is a list of characters enclosed by [ and ].  It
       matches any single character in that list.  If the first  character  of
       the  list is the caret ^ then it matches any character not in the list;
       it is unspecified whether it matches an encoding error.   For  example,
       the regular expression [0123456789] matches any single digit.

       Within  a  bracket  expression,  a  range  expression  consists  of two
       characters separated by a hyphen.  It matches any single character that
       sorts  between  the  two  characters,  inclusive,  using  the  locale's
       collating sequence and character set.  For example, in  the  default  C
       locale, [a-d] is equivalent to [abcd].  Many locales sort characters in
       dictionary  order,  and  in  these  locales  [a-d]  is  typically   not
       equivalent to [abcd]; it might be equivalent to [aBbCcDd], for example.
       To obtain the traditional interpretation of  bracket  expressions,  you
       can  use the C locale by setting the LC_ALL environment variable to the
       value C.

       Finally, certain named classes  of  characters  are  predefined  within
       bracket expressions, as follows.  Their names are self explanatory, and
       they  are  [:alnum:],  [:alpha:],  [:blank:],   [:cntrl:],   [:digit:],
       [:graph:],  [:lower:],  [:print:], [:punct:], [:space:], [:upper:], and
       [:xdigit:].  For example, [[:alnum:]]  means  the  character  class  of
       numbers  and  letters in the current locale.  In the C locale and ASCII
       character set encoding, this is the same as  [0-9A-Za-z].   (Note  that
       the  brackets  in these class names are part of the symbolic names, and
       must be included in addition to the  brackets  delimiting  the  bracket
       expression.)   Most  meta-characters  lose their special meaning inside
       bracket expressions.  To include a literal ]  place  it  first  in  the
       list.   Similarly,  to include a literal ^ place it anywhere but first.
       Finally, to include a literal - place it last.

   Anchoring
       The caret ^ and the dollar sign $ are meta-characters that respectively
       match the empty string at the beginning and end of a line.

   The Backslash Character and Special Expressions
       The  symbols  \<  and  \>  respectively  match  the empty string at the
       beginning and end of a word.  The symbol \b matches the empty string at
       the  edge  of a word, and \B matches the empty string provided it's not
       at the edge of a word.  The symbol \w is a synonym for [_[:alnum:]] and
       \W is a synonym for [^_[:alnum:]].

   Repetition
       A  regular  expression  may  be  followed  by one of several repetition
       operators:
       ?      The preceding item is optional and matched at most once.
       *      The preceding item will be matched zero or more times.
       +      The preceding item will be matched one or more times.
       {n}    The preceding item is matched exactly n times.
       {n,}   The preceding item is matched n or more times.
       {,m}   The preceding item is matched at most m times.  This  is  a  GNU
              extension.
       {n,m}  The  preceding  item  is  matched at least n times, but not more
              than m times.

   Concatenation
       Two regular expressions may  be  concatenated;  the  resulting  regular
       expression  matches  any  string formed by concatenating two substrings
       that respectively match the concatenated expressions.

   Alternation
       Two regular expressions may be joined by  the  infix  operator  |;  the
       resulting   regular  expression  matches  any  string  matching  either
       alternate expression.

   Precedence
       Repetition takes precedence over concatenation,  which  in  turn  takes
       precedence  over  alternation.   A  whole expression may be enclosed in
       parentheses  to  override   these   precedence   rules   and   form   a
       subexpression.

   Back-references and Subexpressions
       The back-reference \n, where n is a single digit, matches the substring
       previously matched  by  the  nth  parenthesized  subexpression  of  the
       regular expression.

   Basic vs Extended Regular Expressions
       In  basic  regular expressions the meta-characters ?, +, {, |, (, and )
       lose their special meaning; instead use the  backslashed  versions  \?,
       \+, \{, \|, \(, and \).

EXIT STATUS
       Normally the exit status is 0 if a line is selected, 1 if no lines were
       selected, and 2 if an error occurred.  However, if the -q or --quiet or
       --silent  is  used and a line is selected, the exit status is 0 even if
       an error occurred.

ENVIRONMENT
       The  behavior  of  grep  is  affected  by  the  following   environment
       variables.

       The  locale  for  category  LC_foo  is specified by examining the three
       environment variables LC_ALL, LC_foo, LANG, in that order.   The  first
       of  these  variables that is set specifies the locale.  For example, if
       LC_ALL is not set, but LC_MESSAGES is set to pt_BR, then the  Brazilian
       Portuguese  locale  is used for the LC_MESSAGES category.  The C locale
       is used if none of these environment variables are set, if  the  locale
       catalog  is  not  installed,  or if grep was not compiled with national
       language support (NLS).  The shell command locale -a lists locales that
       are currently available.

       GREP_OPTIONS
              This variable specifies default options to be placed in front of
              any explicit options.  As  this  causes  problems  when  writing
              portable  scripts,  this  feature  will  be  removed in a future
              release of grep, and grep warns if it is used.   Please  use  an
              alias or script instead.

       GREP_COLOR
              This  variable  specifies  the  color  used to highlight matched
              (non-empty) text.  It is deprecated in favor of GREP_COLORS, but
              still supported.  The mt, ms, and mc capabilities of GREP_COLORS
              have priority over it.  It can only specify the  color  used  to
              highlight  the  matching  non-empty text in any matching line (a
              selected line when the -v command-line option is omitted,  or  a
              context line when -v is specified).  The default is 01;31, which
              means a bold red  foreground  text  on  the  terminal's  default
              background.

       GREP_COLORS
              Specifies  the  colors  and  other  attributes used to highlight
              various parts of the output.  Its  value  is  a  colon-separated
              list       of       capabilities      that      defaults      to
              ms=01;31:mc=01;31:sl=:cx=:fn=35:ln=32:bn=32:se=36  with  the  rv
              and  ne  boolean  capabilities omitted (i.e., false).  Supported
              capabilities are as follows.

              sl=    SGR substring for whole selected  lines  (i.e.,  matching
                     lines when the -v command-line option is omitted, or non-
                     matching lines when -v is  specified).   If  however  the
                     boolean  rv capability and the -v command-line option are
                     both specified, it  applies  to  context  matching  lines
                     instead.   The  default  is  empty  (i.e., the terminal's
                     default color pair).

              cx=    SGR substring for whole context lines (i.e., non-matching
                     lines  when  the  -v  command-line  option is omitted, or
                     matching lines when -v is  specified).   If  however  the
                     boolean  rv capability and the -v command-line option are
                     both specified, it applies to selected non-matching lines
                     instead.   The  default  is  empty  (i.e., the terminal's
                     default color pair).

              rv     Boolean value that reverses (swaps) the meanings  of  the
                     sl=  and cx= capabilities when the -v command-line option
                     is specified.  The default is false (i.e., the capability
                     is omitted).

              mt=01;31
                     SGR substring for matching non-empty text in any matching
                     line (i.e., a selected  line  when  the  -v  command-line
                     option   is  omitted,  or  a  context  line  when  -v  is
                     specified).  Setting this is equivalent to  setting  both
                     ms=  and mc= at once to the same value.  The default is a
                     bold  red  text  foreground   over   the   current   line
                     background.

              ms=01;31
                     SGR  substring  for matching non-empty text in a selected
                     line.  (This is only used when the -v command-line option
                     is  omitted.)   The  effect  of  the  sl=  (or cx= if rv)
                     capability  remains  active  when  this  kicks  in.   The
                     default  is  a  bold red text foreground over the current
                     line background.

              mc=01;31
                     SGR substring for matching non-empty text  in  a  context
                     line.  (This is only used when the -v command-line option
                     is specified.)  The effect of the  cx=  (or  sl=  if  rv)
                     capability  remains  active  when  this  kicks  in.   The
                     default is a bold red text foreground  over  the  current
                     line background.

              fn=35  SGR  substring for file names prefixing any content line.
                     The  default  is  a  magenta  text  foreground  over  the
                     terminal's default background.

              ln=32  SGR  substring  for  line  numbers  prefixing any content
                     line.  The default is a green text  foreground  over  the
                     terminal's default background.

              bn=32  SGR  substring  for  byte  offsets  prefixing any content
                     line.  The default is a green text  foreground  over  the
                     terminal's default background.

              se=36  SGR  substring  for  separators that are inserted between
                     selected line fields (:), between  context  line  fields,
                     (-),  and  between  groups of adjacent lines when nonzero
                     context is specified (--).  The default is  a  cyan  text
                     foreground over the terminal's default background.

              ne     Boolean  value  that prevents clearing to the end of line
                     using Erase in Line (EL) to Right  (\33[K)  each  time  a
                     colorized  item  ends.   This  is  needed on terminals on
                     which EL is not supported.  It  is  otherwise  useful  on
                     terminals  for  which  the back_color_erase (bce) boolean
                     terminfo capability  does  not  apply,  when  the  chosen
                     highlight colors do not affect the background, or when EL
                     is too slow or causes too much flicker.  The  default  is
                     false (i.e., the capability is omitted).

              Note  that  boolean  capabilities  have  no =... part.  They are
              omitted (i.e., false) by default and become true when specified.

              See  the  Select  Graphic  Rendition  (SGR)   section   in   the
              documentation  of  the  text terminal that is used for permitted
              values  and  their  meaning  as  character  attributes.    These
              substring  values are integers in decimal representation and can
              be concatenated with semicolons.  grep takes care of  assembling
              the  result  into  a  complete  SGR sequence (\33[...m).  Common
              values to concatenate include 1 for bold, 4 for underline, 5 for
              blink,  7 for inverse, 39 for default foreground color, 30 to 37
              for foreground colors, 90 to 97  for  16-color  mode  foreground
              colors,  38;5;0  to  38;5;255  for  88-color and 256-color modes
              foreground colors, 49 for default background color, 40 to 47 for
              background  colors,  100  to  107  for  16-color mode background
              colors, and 48;5;0 to 48;5;255 for 88-color and 256-color  modes
              background colors.

       LC_ALL, LC_COLLATE, LANG
              These  variables specify the locale for the LC_COLLATE category,
              which determines the collating sequence used to interpret  range
              expressions like [a-z].

       LC_ALL, LC_CTYPE, LANG
              These  variables  specify  the locale for the LC_CTYPE category,
              which determines the type of characters, e.g., which  characters
              are  whitespace.   This  category  also determines the character
              encoding, that is, whether text is encoded in UTF-8,  ASCII,  or
              some  other  encoding.  In the C or POSIX locale, all characters
              are encoded  as  a  single  byte  and  every  byte  is  a  valid
              character.

       LC_ALL, LC_MESSAGES, LANG
              These variables specify the locale for the LC_MESSAGES category,
              which determines the language that grep uses for messages.   The
              default C locale uses American English messages.

       POSIXLY_CORRECT
              If  set, grep behaves as POSIX requires; otherwise, grep behaves
              more like other GNU programs.  POSIX requires that options  that
              follow  file  names  must  be treated as file names; by default,
              such options are permuted to the front of the operand  list  and
              are  treated as options.  Also, POSIX requires that unrecognized
              options be diagnosed as “illegal”, but since they are not really
              against  the  law  the default is to diagnose them as “invalid”.
              POSIXLY_CORRECT  also   disables   _N_GNU_nonoption_argv_flags_,
              described below.

       _N_GNU_nonoption_argv_flags_
              (Here  N is grep's numeric process ID.)  If the ith character of
              this environment variable's value is 1, do not consider the  ith
              operand  of  grep to be an option, even if it appears to be one.
              A shell can put  this  variable  in  the  environment  for  each
              command  it  runs,  specifying which operands are the results of
              file name wildcard expansion and therefore should not be treated
              as  options.   This  behavior  is  available only with the GNU C
              library, and only when POSIXLY_CORRECT is not set.

NOTES
       This man page is maintained only fitfully; the  full  documentation  is
       often more up-to-date.

COPYRIGHT
       Copyright 1998-2000, 2002, 2005-2020 Free Software Foundation, Inc.

       This is free software; see the source for copying conditions.  There is
       NO warranty; not even for MERCHANTABILITY or FITNESS FOR  A  PARTICULAR
       PURPOSE.

BUGS
   Reporting Bugs
       Email  bug reports to the bug-reporting address ⟨bug-grep@gnu.org⟩.  An
       email archive ⟨https://lists.gnu.org/mailman/listinfo/bug-grep⟩  and  a
       bug   tracker  ⟨https://debbugs.gnu.org/cgi/pkgreport.cgi?package=grep⟩
       are available.

   Known Bugs
       Large repetition counts in the {n,m} construct may cause  grep  to  use
       lots of memory.  In addition, certain other obscure regular expressions
       require exponential time and space, and may cause grep to  run  out  of
       memory.

       Back-references are very slow, and may require exponential time.

EXAMPLE
       The  following  example  outputs  the location and contents of any line
       containing “f” and ending in “.c”, within all files in the current  di‐
       rectory whose names contain “g” and end in “.h”.  The -n option outputs
       line numbers, the -- argument treats  expansions  of  “*g*.h”  starting
       with “-” as file names not options, and the empty file /dev/null causes
       file names to be output even if only one file name happens to be of the
       form “*g*.h”.

         $ grep -n -- 'f.*\.c$' *g*.h /dev/null
         argmatch.h:1:/* definitions and prototypes for argmatch.c

       The only line that matches is line 1 of argmatch.h.  Note that the reg‐
       ular expression syntax used in the pattern differs  from  the  globbing
       syntax that the shell uses to match file names.

SEE ALSO
   Regular Manual Pages
       awk(1),  cmp(1),  diff(1), find(1), perl(1), sed(1), sort(1), xargs(1),
       read(2), pcre(3), pcresyntax(3), pcrepattern(3), terminfo(5),  glob(7),
       regex(7).

   Full Documentation
       A complete manual ⟨https://www.gnu.org/software/grep/manual/⟩ is avail‐
       able.  If the info and grep programs are  properly  installed  at  your
       site, the command

              info grep

       should give you access to the complete manual.

GNU grep 3.4                      2019-12-29                           GREP(1)
GREP(1)                          User Commands                         GREP(1)

NAME
       grep, egrep, fgrep, rgrep - print lines that match patterns

SYNOPSIS
       grep [OPTION...] PATTERNS [FILE...]
       grep [OPTION...] -e PATTERNS ... [FILE...]
       grep [OPTION...] -f PATTERN_FILE ... [FILE...]

DESCRIPTION
       grep  searches  for  PATTERNS  in  each  FILE.  PATTERNS is one or more
       patterns separated by newline characters, and  grep  prints  each  line
       that  matches a pattern.  Typically PATTERNS should be quoted when grep
       is used in a shell command.

       A FILE of “-”  stands  for  standard  input.   If  no  FILE  is  given,
       recursive  searches  examine  the  working  directory, and nonrecursive
       searches read standard input.

       In addition, the variant programs egrep, fgrep and rgrep are  the  same
       as  grep -E,  grep -F,  and  grep -r, respectively.  These variants are
       deprecated, but are provided for backward compatibility.

OPTIONS
   Generic Program Information
       --help Output a usage message and exit.

       -V, --version
              Output the version number of grep and exit.

   Pattern Syntax
       -E, --extended-regexp
              Interpret PATTERNS as extended regular  expressions  (EREs,  see
              below).

       -F, --fixed-strings
              Interpret PATTERNS as fixed strings, not regular expressions.

       -G, --basic-regexp
              Interpret  PATTERNS  as  basic  regular  expressions  (BREs, see
              below).  This is the default.

       -P, --perl-regexp
              Interpret  PATTERNS  as  Perl-compatible   regular   expressions
              (PCREs).   This option is experimental when combined with the -z
              (--null-data) option, and grep  -P  may  warn  of  unimplemented
              features.

   Matching Control
       -e PATTERNS, --regexp=PATTERNS
              Use  PATTERNS  as the patterns.  If this option is used multiple
              times or is combined with the -f (--file) option, search for all
              patterns  given.   This  option can be used to protect a pattern
              beginning with “-”.

       -f FILE, --file=FILE
              Obtain patterns from FILE, one per line.  If this option is used
              multiple  times  or  is  combined with the -e (--regexp) option,
              search for all patterns given.  The  empty  file  contains  zero
              patterns, and therefore matches nothing.

       -i, --ignore-case
              Ignore  case  distinctions  in  patterns and input data, so that
              characters that differ only in case match each other.

       --no-ignore-case
              Do not ignore case distinctions  in  patterns  and  input  data.
              This is the default.  This option is useful for passing to shell
              scripts that already use -i, to cancel its effects  because  the
              two options override each other.

       -v, --invert-match
              Invert the sense of matching, to select non-matching lines.

       -w, --word-regexp
              Select  only  those  lines  containing  matches  that form whole
              words.  The test is that the matching substring must  either  be
              at  the  beginning  of  the  line,  or  preceded  by  a non-word
              constituent character.  Similarly, it must be either at the  end
              of  the  line  or  followed by a non-word constituent character.
              Word-constituent  characters  are  letters,  digits,   and   the
              underscore.  This option has no effect if -x is also specified.

       -x, --line-regexp
              Select  only  those  matches  that exactly match the whole line.
              For a regular expression pattern, this  is  like  parenthesizing
              the pattern and then surrounding it with ^ and $.

       -y     Obsolete synonym for -i.

   General Output Control
       -c, --count
              Suppress  normal output; instead print a count of matching lines
              for each input file.  With the -v,  --invert-match  option  (see
              below), count non-matching lines.

       --color[=WHEN], --colour[=WHEN]
              Surround   the  matched  (non-empty)  strings,  matching  lines,
              context lines, file  names,  line  numbers,  byte  offsets,  and
              separators  (for fields and groups of context lines) with escape
              sequences to display them in color on the terminal.  The  colors
              are  defined  by  the  environment  variable  GREP_COLORS.   The
              deprecated environment variable GREP_COLOR is  still  supported,
              but  its setting does not have priority.  WHEN is never, always,
              or auto.

       -L, --files-without-match
              Suppress normal output; instead print the  name  of  each  input
              file from which no output would normally have been printed.  The
              scanning will stop on the first match.

       -l, --files-with-matches
              Suppress normal output; instead print the  name  of  each  input
              file  from  which  output would normally have been printed.  The
              scanning will stop on the first match.

       -m NUM, --max-count=NUM
              Stop reading a file after NUM matching lines.  If the  input  is
              standard  input  from a regular file, and NUM matching lines are
              output, grep ensures that the standard input  is  positioned  to
              just  after the last matching line before exiting, regardless of
              the presence of trailing context lines.  This enables a  calling
              process  to resume a search.  When grep stops after NUM matching
              lines, it outputs any trailing context lines.  When  the  -c  or
              --count  option  is  also  used,  grep  does  not output a count
              greater than NUM.  When the -v or --invert-match option is  also
              used, grep stops after outputting NUM non-matching lines.

       -o, --only-matching
              Print  only  the  matched  (non-empty) parts of a matching line,
              with each such part on a separate output line.

       -q, --quiet, --silent
              Quiet;  do  not  write  anything  to  standard   output.    Exit
              immediately  with  zero status if any match is found, even if an
              error was detected.  Also see the -s or --no-messages option.

       -s, --no-messages
              Suppress error messages about nonexistent or unreadable files.

   Output Line Prefix Control
       -b, --byte-offset
              Print the 0-based byte offset within the input file before  each
              line of output.  If -o (--only-matching) is specified, print the
              offset of the matching part itself.

       -H, --with-filename
              Print the file name for each match.  This is  the  default  when
              there is more than one file to search.

       -h, --no-filename
              Suppress  the  prefixing  of  file names on output.  This is the
              default when there is only one file (or only standard input)  to
              search.

       --label=LABEL
              Display  input  actually  coming  from  standard  input as input
              coming from file LABEL.  This can be useful  for  commands  that
              transform  a  file's  contents  before searching, e.g., gzip -cd
              foo.gz | grep --label=foo -H 'some pattern'.  See  also  the  -H
              option.

       -n, --line-number
              Prefix  each  line of output with the 1-based line number within
              its input file.

       -T, --initial-tab
              Make sure that the first character of actual line  content  lies
              on a tab stop, so that the alignment of tabs looks normal.  This
              is useful with options that prefix their output  to  the  actual
              content:  -H,-n,  and  -b.   In order to improve the probability
              that lines from a single file will all start at the same column,
              this also causes the line number and byte offset (if present) to
              be printed in a minimum size field width.

       -u, --unix-byte-offsets
              Report Unix-style byte offsets.   This  switch  causes  grep  to
              report  byte offsets as if the file were a Unix-style text file,
              i.e., with  CR  characters  stripped  off.   This  will  produce
              results  identical  to  running  grep  on  a Unix machine.  This
              option has no effect unless -b option is also used;  it  has  no
              effect on platforms other than MS-DOS and MS-Windows.

       -Z, --null
              Output  a  zero  byte  (the  ASCII NUL character) instead of the
              character that normally follows a file name.  For example,  grep
              -lZ  outputs  a  zero  byte  after each file name instead of the
              usual newline.  This option makes the output  unambiguous,  even
              in the presence of file names containing unusual characters like
              newlines.  This option can  be  used  with  commands  like  find
              -print0,  perl  -0,  sort  -z, and xargs -0 to process arbitrary
              file names, even those that contain newline characters.

   Context Line Control
       -A NUM, --after-context=NUM
              Print NUM  lines  of  trailing  context  after  matching  lines.
              Places   a  line  containing  a  group  separator  (--)  between
              contiguous groups of matches.  With the  -o  or  --only-matching
              option, this has no effect and a warning is given.

       -B NUM, --before-context=NUM
              Print  NUM  lines  of  leading  context  before  matching lines.
              Places  a  line  containing  a  group  separator  (--)   between
              contiguous  groups  of  matches.  With the -o or --only-matching
              option, this has no effect and a warning is given.

       -C NUM, -NUM, --context=NUM
              Print NUM lines of output context.  Places a line  containing  a
              group separator (--) between contiguous groups of matches.  With
              the -o or --only-matching option,  this  has  no  effect  and  a
              warning is given.

   File and Directory Selection
       -a, --text
              Process  a binary file as if it were text; this is equivalent to
              the --binary-files=text option.

       --binary-files=TYPE
              If a file's data or metadata indicate  that  the  file  contains
              binary  data,  assume  that  the file is of type TYPE.  Non-text
              bytes indicate binary data; these are either output  bytes  that
              are  improperly  encoded  for  the current locale, or null input
              bytes when the -z option is not given.

              By default, TYPE is binary, and  grep  suppresses  output  after
              null  input  binary  data  is  discovered, and suppresses output
              lines that contain improperly encoded data.  When some output is
              suppressed,  grep  follows  any  output  with a one-line message
              saying that a binary file matches.

              If TYPE is without-match, when grep discovers null input  binary
              data  it  assumes that the rest of the file does not match; this
              is equivalent to the -I option.

              If TYPE is text, grep processes a binary  file  as  if  it  were
              text; this is equivalent to the -a option.

              When  type  is  binary,  grep  may  treat non-text bytes as line
              terminators even without the -z  option.   This  means  choosing
              binary  versus text can affect whether a pattern matches a file.
              For example, when type is binary the pattern q$  might  match  q
              immediately  followed  by  a  null byte, even though this is not
              matched when type is text.  Conversely, when type is binary  the
              pattern . (period) might not match a null byte.

              Warning:  The  -a  option might output binary garbage, which can
              have nasty side effects if the output is a terminal and  if  the
              terminal driver interprets some of it as commands.  On the other
              hand, when reading files whose text encodings  are  unknown,  it
              can   be  helpful  to  use  -a  or  to  set  LC_ALL='C'  in  the
              environment, in order to find more matches even if  the  matches
              are unsafe for direct display.

       -D ACTION, --devices=ACTION
              If  an  input  file  is  a device, FIFO or socket, use ACTION to
              process it.  By  default,  ACTION  is  read,  which  means  that
              devices are read just as if they were ordinary files.  If ACTION
              is skip, devices are silently skipped.

       -d ACTION, --directories=ACTION
              If an input file is a directory, use ACTION to process  it.   By
              default,  ACTION is read, i.e., read directories just as if they
              were  ordinary  files.   If  ACTION  is  skip,   silently   skip
              directories.   If  ACTION  is recurse, read all files under each
              directory, recursively, following symbolic links  only  if  they
              are on the command line.  This is equivalent to the -r option.

       --exclude=GLOB
              Skip  any  command-line file with a name suffix that matches the
              pattern GLOB, using wildcard matching; a name suffix  is  either
              the  whole name, or a trailing part that starts with a non-slash
              character immediately after a  slash  (/)  in  the  name.   When
              searching  recursively, skip any subfile whose base name matches
              GLOB; the base name is the part after the last slash.  A pattern
              can  use *, ?, and [...] as wildcards, and \ to quote a wildcard
              or backslash character literally.

       --exclude-from=FILE
              Skip files whose base name matches any of  the  file-name  globs
              read  from  FILE  (using  wildcard  matching  as described under
              --exclude).

       --exclude-dir=GLOB
              Skip any command-line directory with a name suffix that  matches
              the   pattern   GLOB.   When  searching  recursively,  skip  any
              subdirectory whose base name matches GLOB.  Ignore any redundant
              trailing slashes in GLOB.

       -I     Process  a  binary  file as if it did not contain matching data;
              this is equivalent to the --binary-files=without-match option.

       --include=GLOB
              Search only files whose base name matches GLOB  (using  wildcard
              matching as described under --exclude).

       -r, --recursive
              Read  all  files  under  each  directory, recursively, following
              symbolic links only if they are on the command line.  Note  that
              if   no  file  operand  is  given,  grep  searches  the  working
              directory.  This is equivalent to the -d recurse option.

       -R, --dereference-recursive
              Read all files under each directory,  recursively.   Follow  all
              symbolic links, unlike -r.

   Other Options
       --line-buffered
              Use  line  buffering  on  output.   This can cause a performance
              penalty.

       -U, --binary
              Treat the file(s) as binary.  By default, under MS-DOS  and  MS-
              Windows,  grep  guesses  whether  a  file  is  text or binary as
              described for the --binary-files option.  If  grep  decides  the
              file  is  a  text  file,  it  strips  the CR characters from the
              original file contents (to make regular expressions with ^ and $
              work   correctly).   Specifying  -U  overrules  this  guesswork,
              causing all  files  to  be  read  and  passed  to  the  matching
              mechanism  verbatim; if the file is a text file with CR/LF pairs
              at  the  end  of  each  line,  this  will  cause  some   regular
              expressions  to  fail.   This  option has no effect on platforms
              other than MS-DOS and MS-Windows.

       -z, --null-data
              Treat  input  and  output  data  as  sequences  of  lines,  each
              terminated by a zero byte (the ASCII NUL character) instead of a
              newline.  Like the -Z or --null option, this option can be  used
              with commands like sort -z to process arbitrary file names.

REGULAR EXPRESSIONS
       A  regular  expression  is  a  pattern that describes a set of strings.
       Regular  expressions  are   constructed   analogously   to   arithmetic
       expressions, by using various operators to combine smaller expressions.

       grep understands three different versions of regular expression syntax:
       “basic” (BRE), “extended” (ERE) and “perl” (PCRE).  In GNU  grep  there
       is  no difference in available functionality between basic and extended
       syntaxes.  In other implementations, basic regular expressions are less
       powerful.   The  following  description  applies  to  extended  regular
       expressions; differences for basic regular expressions  are  summarized
       afterwards.    Perl-compatible   regular  expressions  give  additional
       functionality, and are documented in pcresyntax(3) and  pcrepattern(3),
       but work only if PCRE is available in the system.

       The  fundamental building blocks are the regular expressions that match
       a single character.  Most characters, including all letters and digits,
       are regular expressions that match themselves.  Any meta-character with
       special meaning may be quoted by preceding it with a backslash.

       The period . matches any single character.  It is  unspecified  whether
       it matches an encoding error.

   Character Classes and Bracket Expressions
       A  bracket  expression is a list of characters enclosed by [ and ].  It
       matches any single character in that list.  If the first  character  of
       the  list is the caret ^ then it matches any character not in the list;
       it is unspecified whether it matches an encoding error.   For  example,
       the regular expression [0123456789] matches any single digit.

       Within  a  bracket  expression,  a  range  expression  consists  of two
       characters separated by a hyphen.  It matches any single character that
       sorts  between  the  two  characters,  inclusive,  using  the  locale's
       collating sequence and character set.  For example, in  the  default  C
       locale, [a-d] is equivalent to [abcd].  Many locales sort characters in
       dictionary  order,  and  in  these  locales  [a-d]  is  typically   not
       equivalent to [abcd]; it might be equivalent to [aBbCcDd], for example.
       To obtain the traditional interpretation of  bracket  expressions,  you
       can  use the C locale by setting the LC_ALL environment variable to the
       value C.

       Finally, certain named classes  of  characters  are  predefined  within
       bracket expressions, as follows.  Their names are self explanatory, and
       they  are  [:alnum:],  [:alpha:],  [:blank:],   [:cntrl:],   [:digit:],
       [:graph:],  [:lower:],  [:print:], [:punct:], [:space:], [:upper:], and
       [:xdigit:].  For example, [[:alnum:]]  means  the  character  class  of
       numbers  and  letters in the current locale.  In the C locale and ASCII
       character set encoding, this is the same as  [0-9A-Za-z].   (Note  that
       the  brackets  in these class names are part of the symbolic names, and
       must be included in addition to the  brackets  delimiting  the  bracket
       expression.)   Most  meta-characters  lose their special meaning inside
       bracket expressions.  To include a literal ]  place  it  first  in  the
       list.   Similarly,  to include a literal ^ place it anywhere but first.
       Finally, to include a literal - place it last.

   Anchoring
       The caret ^ and the dollar sign $ are meta-characters that respectively
       match the empty string at the beginning and end of a line.

   The Backslash Character and Special Expressions
       The  symbols  \<  and  \>  respectively  match  the empty string at the
       beginning and end of a word.  The symbol \b matches the empty string at
       the  edge  of a word, and \B matches the empty string provided it's not
       at the edge of a word.  The symbol \w is a synonym for [_[:alnum:]] and
       \W is a synonym for [^_[:alnum:]].

   Repetition
       A  regular  expression  may  be  followed  by one of several repetition
       operators:
       ?      The preceding item is optional and matched at most once.
       *      The preceding item will be matched zero or more times.
       +      The preceding item will be matched one or more times.
       {n}    The preceding item is matched exactly n times.
       {n,}   The preceding item is matched n or more times.
       {,m}   The preceding item is matched at most m times.  This  is  a  GNU
              extension.
       {n,m}  The  preceding  item  is  matched at least n times, but not more
              than m times.

   Concatenation
       Two regular expressions may  be  concatenated;  the  resulting  regular
       expression  matches  any  string formed by concatenating two substrings
       that respectively match the concatenated expressions.

   Alternation
       Two regular expressions may be joined by  the  infix  operator  |;  the
       resulting   regular  expression  matches  any  string  matching  either
       alternate expression.

   Precedence
       Repetition takes precedence over concatenation,  which  in  turn  takes
       precedence  over  alternation.   A  whole expression may be enclosed in
       parentheses  to  override   these   precedence   rules   and   form   a
       subexpression.

   Back-references and Subexpressions
       The back-reference \n, where n is a single digit, matches the substring
       previously matched  by  the  nth  parenthesized  subexpression  of  the
       regular expression.

   Basic vs Extended Regular Expressions
       In  basic  regular expressions the meta-characters ?, +, {, |, (, and )
       lose their special meaning; instead use the  backslashed  versions  \?,
       \+, \{, \|, \(, and \).

EXIT STATUS
       Normally the exit status is 0 if a line is selected, 1 if no lines were
       selected, and 2 if an error occurred.  However, if the -q or --quiet or
       --silent  is  used and a line is selected, the exit status is 0 even if
       an error occurred.

ENVIRONMENT
       The  behavior  of  grep  is  affected  by  the  following   environment
       variables.

       The  locale  for  category  LC_foo  is specified by examining the three
       environment variables LC_ALL, LC_foo, LANG, in that order.   The  first
       of  these  variables that is set specifies the locale.  For example, if
       LC_ALL is not set, but LC_MESSAGES is set to pt_BR, then the  Brazilian
       Portuguese  locale  is used for the LC_MESSAGES category.  The C locale
       is used if none of these environment variables are set, if  the  locale
       catalog  is  not  installed,  or if grep was not compiled with national
       language support (NLS).  The shell command locale -a lists locales that
       are currently available.

       GREP_OPTIONS
              This variable specifies default options to be placed in front of
              any explicit options.  As  this  causes  problems  when  writing
              portable  scripts,  this  feature  will  be  removed in a future
              release of grep, and grep warns if it is used.   Please  use  an
              alias or script instead.

       GREP_COLOR
              This  variable  specifies  the  color  used to highlight matched
              (non-empty) text.  It is deprecated in favor of GREP_COLORS, but
              still supported.  The mt, ms, and mc capabilities of GREP_COLORS
              have priority over it.  It can only specify the  color  used  to
              highlight  the  matching  non-empty text in any matching line (a
              selected line when the -v command-line option is omitted,  or  a
              context line when -v is specified).  The default is 01;31, which
              means a bold red  foreground  text  on  the  terminal's  default
              background.

       GREP_COLORS
              Specifies  the  colors  and  other  attributes used to highlight
              various parts of the output.  Its  value  is  a  colon-separated
              list       of       capabilities      that      defaults      to
              ms=01;31:mc=01;31:sl=:cx=:fn=35:ln=32:bn=32:se=36  with  the  rv
              and  ne  boolean  capabilities omitted (i.e., false).  Supported
              capabilities are as follows.

              sl=    SGR substring for whole selected  lines  (i.e.,  matching
                     lines when the -v command-line option is omitted, or non-
                     matching lines when -v is  specified).   If  however  the
                     boolean  rv capability and the -v command-line option are
                     both specified, it  applies  to  context  matching  lines
                     instead.   The  default  is  empty  (i.e., the terminal's
                     default color pair).

              cx=    SGR substring for whole context lines (i.e., non-matching
                     lines  when  the  -v  command-line  option is omitted, or
                     matching lines when -v is  specified).   If  however  the
                     boolean  rv capability and the -v command-line option are
                     both specified, it applies to selected non-matching lines
                     instead.   The  default  is  empty  (i.e., the terminal's
                     default color pair).

              rv     Boolean value that reverses (swaps) the meanings  of  the
                     sl=  and cx= capabilities when the -v command-line option
                     is specified.  The default is false (i.e., the capability
                     is omitted).

              mt=01;31
                     SGR substring for matching non-empty text in any matching
                     line (i.e., a selected  line  when  the  -v  command-line
                     option   is  omitted,  or  a  context  line  when  -v  is
                     specified).  Setting this is equivalent to  setting  both
                     ms=  and mc= at once to the same value.  The default is a
                     bold  red  text  foreground   over   the   current   line
                     background.

              ms=01;31
                     SGR  substring  for matching non-empty text in a selected
                     line.  (This is only used when the -v command-line option
                     is  omitted.)   The  effect  of  the  sl=  (or cx= if rv)
                     capability  remains  active  when  this  kicks  in.   The
                     default  is  a  bold red text foreground over the current
                     line background.

              mc=01;31
                     SGR substring for matching non-empty text  in  a  context
                     line.  (This is only used when the -v command-line option
                     is specified.)  The effect of the  cx=  (or  sl=  if  rv)
                     capability  remains  active  when  this  kicks  in.   The
                     default is a bold red text foreground  over  the  current
                     line background.

              fn=35  SGR  substring for file names prefixing any content line.
                     The  default  is  a  magenta  text  foreground  over  the
                     terminal's default background.

              ln=32  SGR  substring  for  line  numbers  prefixing any content
                     line.  The default is a green text  foreground  over  the
                     terminal's default background.

              bn=32  SGR  substring  for  byte  offsets  prefixing any content
                     line.  The default is a green text  foreground  over  the
                     terminal's default background.

              se=36  SGR  substring  for  separators that are inserted between
                     selected line fields (:), between  context  line  fields,
                     (-),  and  between  groups of adjacent lines when nonzero
                     context is specified (--).  The default is  a  cyan  text
                     foreground over the terminal's default background.

              ne     Boolean  value  that prevents clearing to the end of line
                     using Erase in Line (EL) to Right  (\33[K)  each  time  a
                     colorized  item  ends.   This  is  needed on terminals on
                     which EL is not supported.  It  is  otherwise  useful  on
                     terminals  for  which  the back_color_erase (bce) boolean
                     terminfo capability  does  not  apply,  when  the  chosen
                     highlight colors do not affect the background, or when EL
                     is too slow or causes too much flicker.  The  default  is
                     false (i.e., the capability is omitted).

              Note  that  boolean  capabilities  have  no =... part.  They are
              omitted (i.e., false) by default and become true when specified.

              See  the  Select  Graphic  Rendition  (SGR)   section   in   the
              documentation  of  the  text terminal that is used for permitted
              values  and  their  meaning  as  character  attributes.    These
              substring  values are integers in decimal representation and can
              be concatenated with semicolons.  grep takes care of  assembling
              the  result  into  a  complete  SGR sequence (\33[...m).  Common
              values to concatenate include 1 for bold, 4 for underline, 5 for
              blink,  7 for inverse, 39 for default foreground color, 30 to 37
              for foreground colors, 90 to 97  for  16-color  mode  foreground
              colors,  38;5;0  to  38;5;255  for  88-color and 256-color modes
              foreground colors, 49 for default background color, 40 to 47 for
              background  colors,  100  to  107  for  16-color mode background
              colors, and 48;5;0 to 48;5;255 for 88-color and 256-color  modes
              background colors.

       LC_ALL, LC_COLLATE, LANG
              These  variables specify the locale for the LC_COLLATE category,
              which determines the collating sequence used to interpret  range
              expressions like [a-z].

       LC_ALL, LC_CTYPE, LANG
              These  variables  specify  the locale for the LC_CTYPE category,
              which determines the type of characters, e.g., which  characters
              are  whitespace.   This  category  also determines the character
              encoding, that is, whether text is encoded in UTF-8,  ASCII,  or
              some  other  encoding.  In the C or POSIX locale, all characters
              are encoded  as  a  single  byte  and  every  byte  is  a  valid
              character.

       LC_ALL, LC_MESSAGES, LANG
              These variables specify the locale for the LC_MESSAGES category,
              which determines the language that grep uses for messages.   The
              default C locale uses American English messages.

       POSIXLY_CORRECT
              If  set, grep behaves as POSIX requires; otherwise, grep behaves
              more like other GNU programs.  POSIX requires that options  that
              follow  file  names  must  be treated as file names; by default,
              such options are permuted to the front of the operand  list  and
              are  treated as options.  Also, POSIX requires that unrecognized
              options be diagnosed as “illegal”, but since they are not really
              against  the  law  the default is to diagnose them as “invalid”.
              POSIXLY_CORRECT  also   disables   _N_GNU_nonoption_argv_flags_,
              described below.

       _N_GNU_nonoption_argv_flags_
              (Here  N is grep's numeric process ID.)  If the ith character of
              this environment variable's value is 1, do not consider the  ith
              operand  of  grep to be an option, even if it appears to be one.
              A shell can put  this  variable  in  the  environment  for  each
              command  it  runs,  specifying which operands are the results of
              file name wildcard expansion and therefore should not be treated
              as  options.   This  behavior  is  available only with the GNU C
              library, and only when POSIXLY_CORRECT is not set.

NOTES
       This man page is maintained only fitfully; the  full  documentation  is
       often more up-to-date.

COPYRIGHT
       Copyright 1998-2000, 2002, 2005-2020 Free Software Foundation, Inc.

       This is free software; see the source for copying conditions.  There is
       NO warranty; not even for MERCHANTABILITY or FITNESS FOR  A  PARTICULAR
       PURPOSE.

BUGS
   Reporting Bugs
       Email  bug reports to the bug-reporting address ⟨bug-grep@gnu.org⟩.  An
       email archive ⟨https://lists.gnu.org/mailman/listinfo/bug-grep⟩  and  a
       bug   tracker  ⟨https://debbugs.gnu.org/cgi/pkgreport.cgi?package=grep⟩
       are available.

   Known Bugs
       Large repetition counts in the {n,m} construct may cause  grep  to  use
       lots of memory.  In addition, certain other obscure regular expressions
       require exponential time and space, and may cause grep to  run  out  of
       memory.

       Back-references are very slow, and may require exponential time.

EXAMPLE
       The  following  example  outputs  the location and contents of any line
       containing “f” and ending in “.c”, within all files in the current  di‐
       rectory whose names contain “g” and end in “.h”.  The -n option outputs
       line numbers, the -- argument treats  expansions  of  “*g*.h”  starting
       with “-” as file names not options, and the empty file /dev/null causes
       file names to be output even if only one file name happens to be of the
       form “*g*.h”.

         $ grep -n -- 'f.*\.c$' *g*.h /dev/null
         argmatch.h:1:/* definitions and prototypes for argmatch.c

       The only line that matches is line 1 of argmatch.h.  Note that the reg‐
       ular expression syntax used in the pattern differs  from  the  globbing
       syntax that the shell uses to match file names.

SEE ALSO
   Regular Manual Pages
       awk(1),  cmp(1),  diff(1), find(1), perl(1), sed(1), sort(1), xargs(1),
       read(2), pcre(3), pcresyntax(3), pcrepattern(3), terminfo(5),  glob(7),
       regex(7).

   Full Documentation
       A complete manual ⟨https://www.gnu.org/software/grep/manual/⟩ is avail‐
       able.  If the info and grep programs are  properly  installed  at  your
       site, the command

              info grep

       should give you access to the complete manual.

GNU grep 3.4                      2019-12-29                           GREP(1)
LS(1)                            User Commands                           LS(1)

NAME
       ls - list directory contents

SYNOPSIS
       ls [OPTION]... [FILE]...

DESCRIPTION
       List  information  about  the FILEs (the current directory by default).
       Sort entries alphabetically if none of -cftuvSUX nor --sort  is  speci‐
       fied.

       Mandatory  arguments  to  long  options are mandatory for short options
       too.

       -a, --all
              do not ignore entries starting with .

       -A, --almost-all
              do not list implied . and ..

       --author
              with -l, print the author of each file

       -b, --escape
              print C-style escapes for nongraphic characters

       --block-size=SIZE
              with  -l,  scale  sizes  by  SIZE  when  printing  them;   e.g.,
              '--block-size=M'; see SIZE format below

       -B, --ignore-backups
              do not list implied entries ending with ~

       -c     with -lt: sort by, and show, ctime (time of last modification of
              file status information); with -l: show ctime and sort by  name;
              otherwise: sort by ctime, newest first

       -C     list entries by columns

       --color[=WHEN]
              colorize  the output; WHEN can be 'always' (default if omitted),
              'auto', or 'never'; more info below

       -d, --directory
              list directories themselves, not their contents

       -D, --dired
              generate output designed for Emacs' dired mode

       -f     do not sort, enable -aU, disable -ls --color

       -F, --classify
              append indicator (one of */=>@|) to entries

       --file-type
              likewise, except do not append '*'

       --format=WORD
              across -x, commas -m, horizontal -x, long -l, single-column  -1,
              verbose -l, vertical -C

       --full-time
              like -l --time-style=full-iso

       -g     like -l, but do not list owner

       --group-directories-first
              group directories before files;

              can   be  augmented  with  a  --sort  option,  but  any  use  of
              --sort=none (-U) disables grouping

       -G, --no-group
              in a long listing, don't print group names

       -h, --human-readable
              with -l and -s, print sizes like 1K 234M 2G etc.

       --si   likewise, but use powers of 1000 not 1024

       -H, --dereference-command-line
              follow symbolic links listed on the command line

       --dereference-command-line-symlink-to-dir
              follow each command line symbolic link

              that points to a directory

       --hide=PATTERN
              do not list implied entries matching shell  PATTERN  (overridden
              by -a or -A)

       --hyperlink[=WHEN]
              hyperlink file names; WHEN can be 'always' (default if omitted),
              'auto', or 'never'

       --indicator-style=WORD
              append indicator with style WORD to entry names: none (default),
              slash (-p), file-type (--file-type), classify (-F)

       -i, --inode
              print the index number of each file

       -I, --ignore=PATTERN
              do not list implied entries matching shell PATTERN

       -k, --kibibytes
              default  to  1024-byte  blocks for disk usage; used only with -s
              and per directory totals

       -l     use a long listing format

       -L, --dereference
              when showing file information for a symbolic link, show informa‐
              tion  for  the file the link references rather than for the link
              itself

       -m     fill width with a comma separated list of entries

       -n, --numeric-uid-gid
              like -l, but list numeric user and group IDs

       -N, --literal
              print entry names without quoting

       -o     like -l, but do not list group information

       -p, --indicator-style=slash
              append / indicator to directories

       -q, --hide-control-chars
              print ? instead of nongraphic characters

       --show-control-chars
              show nongraphic characters as-is (the default, unless program is
              'ls' and output is a terminal)

       -Q, --quote-name
              enclose entry names in double quotes

       --quoting-style=WORD
              use  quoting style WORD for entry names: literal, locale, shell,
              shell-always,  shell-escape,  shell-escape-always,   c,   escape
              (overrides QUOTING_STYLE environment variable)

       -r, --reverse
              reverse order while sorting

       -R, --recursive
              list subdirectories recursively

       -s, --size
              print the allocated size of each file, in blocks

       -S     sort by file size, largest first

       --sort=WORD
              sort  by  WORD instead of name: none (-U), size (-S), time (-t),
              version (-v), extension (-X)

       --time=WORD
              with -l, show time as WORD instead of default modification time:
              atime  or  access  or  use  (-u); ctime or status (-c); also use
              specified time as sort key if --sort=time (newest first)

       --time-style=TIME_STYLE
              time/date format with -l; see TIME_STYLE below

       -t     sort by modification time, newest first

       -T, --tabsize=COLS
              assume tab stops at each COLS instead of 8

       -u     with -lt: sort by, and show, access time; with -l:  show  access
              time  and  sort  by name; otherwise: sort by access time, newest
              first

       -U     do not sort; list entries in directory order

       -v     natural sort of (version) numbers within text

       -w, --width=COLS
              set output width to COLS.  0 means no limit

       -x     list entries by lines instead of by columns

       -X     sort alphabetically by entry extension

       -Z, --context
              print any security context of each file

       -1     list one file per line.  Avoid '\n' with -q or -b

       --help display this help and exit

       --version
              output version information and exit

       The SIZE argument is an integer and  optional  unit  (example:  10K  is
       10*1024).   Units  are  K,M,G,T,P,E,Z,Y  (powers  of 1024) or KB,MB,...
       (powers of 1000).

       The TIME_STYLE argument can be  full-iso,  long-iso,  iso,  locale,  or
       +FORMAT.   FORMAT  is  interpreted  like in date(1).  If FORMAT is FOR‐
       MAT1<newline>FORMAT2, then FORMAT1 applies to non-recent files and FOR‐
       MAT2  to  recent files.  TIME_STYLE prefixed with 'posix-' takes effect
       only outside the POSIX locale.  Also the TIME_STYLE  environment  vari‐
       able sets the default style to use.

       Using  color  to distinguish file types is disabled both by default and
       with --color=never.  With --color=auto, ls emits color codes only  when
       standard  output is connected to a terminal.  The LS_COLORS environment
       variable can change the settings.  Use the dircolors command to set it.

   Exit status:
       0      if OK,

       1      if minor problems (e.g., cannot access subdirectory),

       2      if serious trouble (e.g., cannot access command-line argument).

AUTHOR
       Written by Richard M. Stallman and David MacKenzie.

REPORTING BUGS
       GNU coreutils online help: <https://www.gnu.org/software/coreutils/>
       Report ls translation bugs to <https://translationproject.org/team/>

COPYRIGHT
       Copyright © 2018 Free Software Foundation, Inc.   License  GPLv3+:  GNU
       GPL version 3 or later <https://gnu.org/licenses/gpl.html>.
       This  is  free  software:  you  are free to change and redistribute it.
       There is NO WARRANTY, to the extent permitted by law.

SEE ALSO
       Full documentation at: <https://www.gnu.org/software/coreutils/ls>
       or available locally via: info '(coreutils) ls invocation'

GNU coreutils 8.30              September 2019                           LS(1)
SELECT(2)                  Linux Programmer's Manual                 SELECT(2)

NAME
       select,  pselect,  FD_CLR,  FD_ISSET, FD_SET, FD_ZERO - synchronous I/O
       multiplexing

SYNOPSIS
       /* According to POSIX.1-2001, POSIX.1-2008 */
       #include <sys/select.h>

       /* According to earlier standards */
       #include <sys/time.h>
       #include <sys/types.h>
       #include <unistd.h>

       int select(int nfds, fd_set *readfds, fd_set *writefds,
                  fd_set *exceptfds, struct timeval *timeout);

       void FD_CLR(int fd, fd_set *set);
       int  FD_ISSET(int fd, fd_set *set);
       void FD_SET(int fd, fd_set *set);
       void FD_ZERO(fd_set *set);

       #include <sys/select.h>

       int pselect(int nfds, fd_set *readfds, fd_set *writefds,
                   fd_set *exceptfds, const struct timespec *timeout,
                   const sigset_t *sigmask);

   Feature Test Macro Requirements for glibc (see feature_test_macros(7)):

       pselect(): _POSIX_C_SOURCE >= 200112L

DESCRIPTION
       select() and pselect() allow a program to  monitor  multiple  file  de‐
       scriptors,  waiting  until  one  or more of the file descriptors become
       "ready" for some class of I/O operation (e.g., input possible).  A file
       descriptor  is  considered  ready if it is possible to perform a corre‐
       sponding  I/O  operation  (e.g.,  read(2),  or  a  sufficiently   small
       write(2)) without blocking.

       select()  can  monitor only file descriptors numbers that are less than
       FD_SETSIZE; poll(2) does not have this limitation.  See BUGS.

       The operation of select() and pselect() is identical, other than  these
       three differences:

       (i)    select()  uses  a timeout that is a struct timeval (with seconds
              and microseconds), while pselect() uses a struct timespec  (with
              seconds and nanoseconds).

       (ii)   select()  may  update  the timeout argument to indicate how much
              time was left.  pselect() does not change this argument.

       (iii)  select() has no  sigmask  argument,  and  behaves  as  pselect()
              called with NULL sigmask.

       Three  independent  sets of file descriptors are watched.  The file de‐
       scriptors listed in readfds will be watched to see if characters become
       available for reading (more precisely, to see if a read will not block;
       in particular, a file descriptor is also ready  on  end-of-file).   The
       file  descriptors in writefds will be watched to see if space is avail‐
       able for write (though a large write may still block).   The  file  de‐
       scriptors  in  exceptfds  will  be  watched for exceptional conditions.
       (For examples of some exceptional conditions,  see  the  discussion  of
       POLLPRI in poll(2).)

       On exit, each of the file descriptor sets is modified in place to indi‐
       cate which file descriptors actually changed status.  (Thus,  if  using
       select()  within  a  loop,  the  sets must be reinitialized before each
       call.)

       Each of the three file descriptor sets may be specified as NULL  if  no
       file  descriptors  are  to  be  watched  for the corresponding class of
       events.

       Four macros are provided to manipulate the sets.   FD_ZERO()  clears  a
       set.  FD_SET() and FD_CLR() add and remove a given file descriptor from
       a set.  FD_ISSET() tests to see if a file descriptor  is  part  of  the
       set; this is useful after select() returns.

       nfds  should  be  set to the highest-numbered file descriptor in any of
       the three sets, plus 1.  The indicated file descriptors in each set are
       checked, up to this limit (but see BUGS).

       The  timeout argument specifies the interval that select() should block
       waiting for a file descriptor to become ready.  The call will block un‐
       til either:

       *  a file descriptor becomes ready;

       *  the call is interrupted by a signal handler; or

       *  the timeout expires.

       Note  that  the timeout interval will be rounded up to the system clock
       granularity, and kernel scheduling delays mean that the blocking inter‐
       val  may  overrun  by  a  small  amount.  If both fields of the timeval
       structure are zero, then select() returns immediately.  (This is useful
       for  polling.)  If timeout is NULL (no timeout), select() can block in‐
       definitely.

       sigmask is a pointer to a signal mask (see sigprocmask(2));  if  it  is
       not  NULL, then pselect() first replaces the current signal mask by the
       one pointed to by sigmask, then does the "select"  function,  and  then
       restores the original signal mask.

       Other than the difference in the precision of the timeout argument, the
       following pselect() call:

           ready = pselect(nfds, &readfds, &writefds, &exceptfds,
                           timeout, &sigmask);

       is equivalent to atomically executing the following calls:

           sigset_t origmask;

           pthread_sigmask(SIG_SETMASK, &sigmask, &origmask);
           ready = select(nfds, &readfds, &writefds, &exceptfds, timeout);
           pthread_sigmask(SIG_SETMASK, &origmask, NULL);

       The reason that pselect() is needed is that if one wants  to  wait  for
       either  a  signal  or  for  a  file descriptor to become ready, then an
       atomic test is needed to prevent race conditions.  (Suppose the  signal
       handler  sets  a  global  flag and returns.  Then a test of this global
       flag followed by a call of select() could hang indefinitely if the sig‐
       nal arrived just after the test but just before the call.  By contrast,
       pselect() allows one to first block signals, handle  the  signals  that
       have  come  in,  then call pselect() with the desired sigmask, avoiding
       the race.)

   The timeout
       The time structures involved are defined in <sys/time.h> and look like

           struct timeval {
               long    tv_sec;         /* seconds */
               long    tv_usec;        /* microseconds */
           };

       and

           struct timespec {
               long    tv_sec;         /* seconds */
               long    tv_nsec;        /* nanoseconds */
           };

       (However, see below on the POSIX.1 versions.)

       Some code calls select() with all three sets empty, nfds  zero,  and  a
       non-NULL  timeout as a fairly portable way to sleep with subsecond pre‐
       cision.

       On Linux, select() modifies timeout to reflect the amount of  time  not
       slept; most other implementations do not do this.  (POSIX.1 permits ei‐
       ther behavior.)  This causes problems both when Linux code which  reads
       timeout  is  ported to other operating systems, and when code is ported
       to Linux that reuses a struct timeval for multiple select()s in a  loop
       without  reinitializing it.  Consider timeout to be undefined after se‐
       lect() returns.

RETURN VALUE
       On success, select() and pselect() return the number of  file  descrip‐
       tors  contained in the three returned descriptor sets (that is, the to‐
       tal number of bits that are set in readfds, writefds, exceptfds)  which
       may be zero if the timeout expires before anything interesting happens.
       On error, -1 is returned, and errno is set to indicate the  error;  the
       file descriptor sets are unmodified, and timeout becomes undefined.

ERRORS
       EBADF  An  invalid file descriptor was given in one of the sets.  (Per‐
              haps a file descriptor that was already closed, or one on  which
              an error has occurred.)  However, see BUGS.

       EINTR  A signal was caught; see signal(7).

       EINVAL nfds  is  negative  or  exceeds the RLIMIT_NOFILE resource limit
              (see getrlimit(2)).

       EINVAL The value contained within timeout is invalid.

       ENOMEM Unable to allocate memory for internal tables.

VERSIONS
       pselect() was added to Linux in kernel 2.6.16.   Prior  to  this,  pse‐
       lect() was emulated in glibc (but see BUGS).

CONFORMING TO
       select()  conforms  to POSIX.1-2001, POSIX.1-2008, and 4.4BSD (select()
       first appeared in 4.2BSD).  Generally portable to/from non-BSD  systems
       supporting  clones  of  the  BSD socket layer (including System V vari‐
       ants).  However, note that the  System V  variant  typically  sets  the
       timeout variable before exit, but the BSD variant does not.

       pselect() is defined in POSIX.1g, and in POSIX.1-2001 and POSIX.1-2008.

NOTES
       An  fd_set is a fixed size buffer.  Executing FD_CLR() or FD_SET() with
       a value of fd that is negative or is equal to or larger than FD_SETSIZE
       will result in undefined behavior.  Moreover, POSIX requires fd to be a
       valid file descriptor.

       The operation of select() and pselect() is not affected by  the  O_NON‐
       BLOCK flag.

       On  some other UNIX systems, select() can fail with the error EAGAIN if
       the system fails to allocate  kernel-internal  resources,  rather  than
       ENOMEM  as Linux does.  POSIX specifies this error for poll(2), but not
       for select().  Portable programs may wish to check for EAGAIN and loop,
       just as with EINTR.

       On  systems  that  lack  pselect(), reliable (and more portable) signal
       trapping can be achieved using the self-pipe trick.  In this technique,
       a  signal  handler writes a byte to a pipe whose other end is monitored
       by select() in the main program.   (To  avoid  possibly  blocking  when
       writing  to  a pipe that may be full or reading from a pipe that may be
       empty, nonblocking I/O is used when reading from  and  writing  to  the
       pipe.)

       Concerning  the types involved, the classical situation is that the two
       fields of a timeval structure are typed as long (as shown  above),  and
       the structure is defined in <sys/time.h>.  The POSIX.1 situation is

           struct timeval {
               time_t         tv_sec;     /* seconds */
               suseconds_t    tv_usec;    /* microseconds */
           };

       where  the  structure  is  defined in <sys/select.h> and the data types
       time_t and suseconds_t are defined in <sys/types.h>.

       Concerning prototypes, the classical situation is that one  should  in‐
       clude  <time.h> for select().  The POSIX.1 situation is that one should
       include <sys/select.h> for select() and pselect().

       Under glibc 2.0, <sys/select.h> gives  the  wrong  prototype  for  pse‐
       lect().   Under glibc 2.1 to 2.2.1, it gives pselect() when _GNU_SOURCE
       is defined.  Since glibc 2.2.2, the requirements are as  shown  in  the
       SYNOPSIS.

   Correspondence between select() and poll() notifications
       Within the Linux kernel source, we find the following definitions which
       show the correspondence between the readable, writable, and exceptional
       condition  notifications  of  select() and the event notifications pro‐
       vided by poll(2) and epoll(7):

           #define POLLIN_SET  (EPOLLRDNORM | EPOLLRDBAND | EPOLLIN |
                                EPOLLHUP | EPOLLERR)
                              /* Ready for reading */
           #define POLLOUT_SET (EPOLLWRBAND | EPOLLWRNORM | EPOLLOUT |
                                EPOLLERR)
                              /* Ready for writing */
           #define POLLEX_SET  (EPOLLPRI)
                              /* Exceptional condition */

   Multithreaded applications
       If a file descriptor being monitored by select() is closed  in  another
       thread,  the result is unspecified.  On some UNIX systems, select() un‐
       blocks and returns, with an indication  that  the  file  descriptor  is
       ready  (a  subsequent I/O operation will likely fail with an error, un‐
       less another process reopens file descriptor between the time  select()
       returned and the I/O operation is performed).  On Linux (and some other
       systems), closing the file descriptor in another thread has  no  effect
       on  select().   In summary, any application that relies on a particular
       behavior in this scenario must be considered buggy.

   C library/kernel differences
       The Linux kernel allows file descriptor sets of arbitrary size,  deter‐
       mining  the  length  of  the sets to be checked from the value of nfds.
       However, in the glibc implementation, the fd_set type is fixed in size.
       See also BUGS.

       The pselect() interface described in this page is implemented by glibc.
       The underlying Linux system call is named pselect6().  This system call
       has somewhat different behavior from the glibc wrapper function.

       The  Linux  pselect6() system call modifies its timeout argument.  How‐
       ever, the glibc wrapper function hides this behavior by using  a  local
       variable  for  the  timeout argument that is passed to the system call.
       Thus, the glibc pselect() function does not modify  its  timeout  argu‐
       ment; this is the behavior required by POSIX.1-2001.

       The  final  argument  of the pselect6() system call is not a sigset_t *
       pointer, but is instead a structure of the form:

           struct {
               const kernel_sigset_t *ss;   /* Pointer to signal set */
               size_t ss_len;               /* Size (in bytes) of object
                                               pointed to by 'ss' */
           };

       This allows the system call to obtain both a pointer to the signal  set
       and  its size, while allowing for the fact that most architectures sup‐
       port a maximum of 6 arguments to a system call.  See sigprocmask(2) for
       a  discussion  of  the difference between the kernel and libc notion of
       the signal set.

BUGS
       POSIX allows an implementation to define an upper limit, advertised via
       the  constant  FD_SETSIZE, on the range of file descriptors that can be
       specified in a file descriptor set.  The Linux kernel imposes no  fixed
       limit,  but  the  glibc  implementation makes fd_set a fixed-size type,
       with FD_SETSIZE defined as 1024, and the FD_*()  macros  operating  ac‐
       cording  to that limit.  To monitor file descriptors greater than 1023,
       use poll(2) instead.

       The implementation of the fd_set arguments  as  value-result  arguments
       means  that  they must be reinitialized on each call to select().  This
       design error is avoided  by  poll(2),  which  uses  separate  structure
       fields for the input and output of the call.

       According  to  POSIX, select() should check all specified file descrip‐
       tors in the three file descriptor sets, up to the limit  nfds-1.   How‐
       ever,  the  current implementation ignores any file descriptor in these
       sets that is greater than the maximum file descriptor number  that  the
       process currently has open.  According to POSIX, any such file descrip‐
       tor that is specified in one of the sets should  result  in  the  error
       EBADF.

       Glibc  2.0  provided a version of pselect() that did not take a sigmask
       argument.

       Starting with version 2.1, glibc provided  an  emulation  of  pselect()
       that was implemented using sigprocmask(2) and select().  This implemen‐
       tation remained vulnerable to the very race  condition  that  pselect()
       was  designed to prevent.  Modern versions of glibc use the (race-free)
       pselect() system call on kernels where it is provided.

       Under Linux, select() may report a socket file descriptor as "ready for
       reading",  while nevertheless a subsequent read blocks.  This could for
       example happen when data has arrived but  upon  examination  has  wrong
       checksum and is discarded.  There may be other circumstances in which a
       file descriptor is spuriously reported as ready.  Thus it may be  safer
       to use O_NONBLOCK on sockets that should not block.

       On  Linux, select() also modifies timeout if the call is interrupted by
       a signal handler (i.e., the EINTR error return).  This is not permitted
       by POSIX.1.  The Linux pselect() system call has the same behavior, but
       the glibc wrapper hides this behavior by internally copying the timeout
       to a local variable and passing that variable to the system call.

EXAMPLE
       #include <stdio.h>
       #include <stdlib.h>
       #include <sys/time.h>
       #include <sys/types.h>
       #include <unistd.h>

       int
       main(void)
       {
           fd_set rfds;
           struct timeval tv;
           int retval;

           /* Watch stdin (fd 0) to see when it has input. */

           FD_ZERO(&rfds);
           FD_SET(0, &rfds);

           /* Wait up to five seconds. */

           tv.tv_sec = 5;
           tv.tv_usec = 0;

           retval = select(1, &rfds, NULL, NULL, &tv);
           /* Don't rely on the value of tv now! */

           if (retval == -1)
               perror("select()");
           else if (retval)
               printf("Data is available now.\n");
               /* FD_ISSET(0, &rfds) will be true. */
           else
               printf("No data within five seconds.\n");

           exit(EXIT_SUCCESS);
       }

SEE ALSO
       accept(2),  connect(2),  poll(2), read(2), recv(2), restart_syscall(2),
       send(2), sigprocmask(2), write(2), epoll(7), time(7)

       For a tutorial with discussion and examples, see select_tut(2).

COLOPHON
       This page is part of release 5.05 of the Linux  man-pages  project.   A
       description  of  the project, information about reporting bugs, and the
       latest    version    of    this    page,    can     be     found     at
       https://www.kernel.org/doc/man-pages/.

Linux                             2019-11-19                         SELECT(2)
DO(7)                    PostgreSQL 16.3 Documentation                   DO(7)

NAME
       DO - execute an anonymous code block

SYNOPSIS
       DO [ LANGUAGE lang_name ] code

DESCRIPTION
       DO executes an anonymous code block, or in other words a transient
       anonymous function in a procedural language.

       The code block is treated as though it were the body of a function with
       no parameters, returning void. It is parsed and executed a single time.

       The optional LANGUAGE clause can be written either before or after the
       code block.

PARAMETERS
       code
           The procedural language code to be executed. This must be specified
           as a string literal, just as in CREATE FUNCTION. Use of a
           dollar-quoted literal is recommended.

       lang_name
           The name of the procedural language the code is written in. If
           omitted, the default is plpgsql.

NOTES
       The procedural language to be used must already have been installed
       into the current database by means of CREATE EXTENSION.  plpgsql is
       installed by default, but other languages are not.

       The user must have USAGE privilege for the procedural language, or must
       be a superuser if the language is untrusted. This is the same privilege
       requirement as for creating a function in the language.

       If DO is executed in a transaction block, then the procedure code
       cannot execute transaction control statements. Transaction control
       statements are only allowed if DO is executed in its own transaction.

EXAMPLES
       Grant all privileges on all views in schema public to role webuser:

           DO $$DECLARE r record;
           BEGIN
               FOR r IN SELECT table_schema, table_name FROM information_schema.tables
                        WHERE table_type = 'VIEW' AND table_schema = 'public'
               LOOP
                   EXECUTE 'GRANT ALL ON ' || quote_ident(r.table_schema) || '.' || quote_ident(r.table_name) || ' TO webuser';
               END LOOP;
           END$$;

COMPATIBILITY
       There is no DO statement in the SQL standard.

SEE ALSO
       CREATE LANGUAGE (CREATE_LANGUAGE(7))

PostgreSQL 16.3                      2024                                DO(7)
TIME(1)                     General Commands Manual                    TIME(1)

NAME
       time - run programs and summarize system resource usage

SYNOPSIS
       time   [ -apqvV ] [ -f FORMAT ] [ -o FILE ]
              [ --append ] [ --verbose ] [ --quiet ] [ --portability ]
              [ --format=FORMAT ] [ --output=FILE ] [ --version ]
              [ --help ] COMMAND [ ARGS ]

DESCRIPTION
       time run the program COMMAND with any given arguments ARG....  When
       COMMAND finishes, time displays information about resources used by
       COMMAND (on the standard error output, by default).  If COMMAND exits
       with non-zero status, time displays a warning message and the exit
       status.

       time determines which information to display about the resources used
       by the COMMAND from the string FORMAT.  If no format is specified on
       the command line, but the TIME environment variable is set, its value
       is used as the format.  Otherwise, a default format built into time is
       used.

       Options to time must appear on the command line before COMMAND.
       Anything on the command line after COMMAND is passed as arguments to
       COMMAND.

OPTIONS
       -o FILE, --output=FILE
              Write the resource use statistics to FILE instead of to the
              standard error stream.  By default, this overwrites the file,
              destroying the file's previous contents.  This option is useful
              for collecting information on interactive programs and programs
              that produce output on the standard error stream.

       -a, --append
              Append the resource use information to the output file instead
              of overwriting it.  This option is only useful with the `-o' or
              `--output' option.

       -f FORMAT, --format FORMAT
              Use FORMAT as the format string that controls the output of
              time.  See the below more information.

       --help Print a summary of the command line options and exit.

       -p, --portability
              Use the following format string, for conformance with POSIX
              standard 1003.2:
                        real %e
                        user %U
                        sys %S

       -v, --verbose
              Use the built-in verbose format, which displays each available
              piece of information on the program's resource use on its own
              line, with an English description of its meaning.

       --quiet
              Do not report the status of the program even if it is different
              from zero.

       -V, --version
              Print the version number of time and exit.

FORMATTING THE OUTPUT
       The format string FORMAT controls the contents of the time output.  The
       format string can be set using the `-f' or `--format', `-v' or
       `--verbose', or `-p' or `--portability' options.  If they are not
       given, but the TIME environment variable is set, its value is used as
       the format string.  Otherwise, a built-in default format is used.  The
       default format is:
         %Uuser %Ssystem %Eelapsed %PCPU (%Xtext+%Ddata %Mmax)k
         %Iinputs+%Ooutputs (%Fmajor+%Rminor)pagefaults %Wswaps

       The format string usually consists of `resource specifiers'
       interspersed with plain text.  A percent sign (`%') in the format
       string causes the following character to be interpreted as a resource
       specifier, which is similar to the formatting characters in the
       printf(3) function.

       A backslash (`\') introduces a `backslash escape', which is translated
       into a single printing character upon output.  `\t' outputs a tab
       character, `\n' outputs a newline, and `\\' outputs a backslash.  A
       backslash followed by any other character outputs a question mark (`?')
       followed by a backslash, to indicate that an invalid backslash escape
       was given.

       Other text in the format string is copied verbatim to the output.  time
       always prints a newline after printing the resource use information, so
       normally format strings do not end with a newline character (or `\n').

       There are many resource specifications.  Not all resources are measured
       by all versions of Unix, so some of the values might be reported as
       zero.  Any character following a percent sign that is not listed in the
       table below causes a question mark (`?') to be output, followed by that
       character, to indicate that an invalid resource specifier was given.

       The resource specifiers, which are a superset of those recognized by
       the tcsh(1) builtin `time' command, are:
              %      A literal `%'.
              C      Name and command line arguments of the command being
                     timed.
              D      Average size of the process's unshared data area, in
                     Kilobytes.
              E      Elapsed real (wall clock) time used by the process, in
                     [hours:]minutes:seconds.
              F      Number of major, or I/O-requiring, page faults that
                     occurred while the process was running.  These are faults
                     where the page has actually migrated out of primary
                     memory.
              I      Number of file system inputs by the process.
              K      Average total (data+stack+text) memory use of the
                     process, in Kilobytes.
              M      Maximum resident set size of the process during its
                     lifetime, in Kilobytes.
              O      Number of file system outputs by the process.
              P      Percentage of the CPU that this job got.  This is just
                     user + system times divided by the total running time.
                     It also prints a percentage sign.
              R      Number of minor, or recoverable, page faults.  These are
                     pages that are not valid (so they fault) but which have
                     not yet been claimed by other virtual pages.  Thus the
                     data in the page is still valid but the system tables
                     must be updated.
              S      Total number of CPU-seconds used by the system on behalf
                     of the process (in kernel mode), in seconds.
              U      Total number of CPU-seconds that the process used
                     directly (in user mode), in seconds.
              W      Number of times the process was swapped out of main
                     memory.
              X      Average amount of shared text in the process, in
                     Kilobytes.
              Z      System's page size, in bytes.  This is a per-system
                     constant, but varies between systems.
              c      Number of times the process was context-switched
                     involuntarily (because the time slice expired).
              e      Elapsed real (wall clock) time used by the process, in
                     seconds.
              k      Number of signals delivered to the process.
              p      Average unshared stack size of the process, in Kilobytes.
              r      Number of socket messages received by the process.
              s      Number of socket messages sent by the process.
              t      Average resident set size of the process, in Kilobytes.
              w      Number of times that the program was context-switched
                     voluntarily, for instance while waiting for an I/O
                     operation to complete.
              x      Exit status of the command.

EXAMPLES
       To run the command `wc /etc/hosts' and show the default information:
            time wc /etc/hosts

       To run the command `ls -Fs' and show just the user, system, and total
       time:
            time -f "\t%E real,\t%U user,\t%S sys" ls -Fs

       To edit the file BORK and have `time' append the elapsed time and
       number of signals to the file `log', reading the format string from the
       environment variable `TIME':
            export TIME="\t%E,\t%k" # If using bash or ksh
            setenv TIME "\t%E,\t%k" # If using csh or tcsh
            time -a -o log emacs bork

       Users of the bash shell need to use an explicit path in order to run
       the external time command and not the shell builtin variant.  On system
       where time is installed in /usr/bin, the first example would become
            /usr/bin/time wc /etc/hosts

ACCURACY
       The elapsed time is not collected atomically with the execution of the
       program; as a result, in bizarre circumstances (if the time command
       gets stopped or swapped out in between when the program being timed
       exits and when time calculates how long it took to run), it could be
       much larger than the actual execution time.

       When the running time of a command is very nearly zero, some values
       (e.g., the percentage of CPU used) may be reported as either zero
       (which is wrong) or a question mark.

       Most information shown by time is derived from the wait3(2) system
       call.  The numbers are only as good as those returned by wait3(2).  On
       systems that do not have a wait3(2) call that returns status
       information, the times(2) system call is used instead.  However, it
       provides much less information than wait3(2), so on those systems time
       reports the majority of the resources as zero.

       The `%I' and `%O' values are allegedly only `real' input and output and
       do not include those supplied by caching devices.  The meaning of
       `real' I/O reported by `%I' and `%O' may be muddled for workstations,
       especially diskless ones.

DIAGNOSTICS
       The time command returns when the program exits, stops, or is
       terminated by a signal.  If the program exited normally, the return
       value of time is the return value of the program it executed and
       measured.  Otherwise, the return value is 128 plus the number of the
       signal which caused the program to stop or terminate.
AUTHOR
       time was written by David MacKenzie.  This man page was added by Dirk
       Eddelbuettel <edd@debian.org>, the Debian GNU/Linux maintainer, for use
       by the Debian GNU/Linux distribution but may of course be used by
       others.

SEE ALSO
       tcsh(1), printf(3)

                               Debian GNU/Linux                        TIME(1)
TEST(1)                          User Commands                         TEST(1)

NAME
       test - check file types and compare values

SYNOPSIS
       test EXPRESSION
       test
       [ EXPRESSION ]
       [ ]
       [ OPTION

DESCRIPTION
       Exit with the status determined by EXPRESSION.

       --help display this help and exit

       --version
              output version information and exit

       An omitted EXPRESSION defaults to false.  Otherwise, EXPRESSION is true
       or false and sets exit status.  It is one of:

       ( EXPRESSION )
              EXPRESSION is true

       ! EXPRESSION
              EXPRESSION is false

       EXPRESSION1 -a EXPRESSION2
              both EXPRESSION1 and EXPRESSION2 are true

       EXPRESSION1 -o EXPRESSION2
              either EXPRESSION1 or EXPRESSION2 is true

       -n STRING
              the length of STRING is nonzero

       STRING equivalent to -n STRING

       -z STRING
              the length of STRING is zero

       STRING1 = STRING2
              the strings are equal

       STRING1 != STRING2
              the strings are not equal

       INTEGER1 -eq INTEGER2
              INTEGER1 is equal to INTEGER2

       INTEGER1 -ge INTEGER2
              INTEGER1 is greater than or equal to INTEGER2

       INTEGER1 -gt INTEGER2
              INTEGER1 is greater than INTEGER2

       INTEGER1 -le INTEGER2
              INTEGER1 is less than or equal to INTEGER2

       INTEGER1 -lt INTEGER2
              INTEGER1 is less than INTEGER2

       INTEGER1 -ne INTEGER2
              INTEGER1 is not equal to INTEGER2

       FILE1 -ef FILE2
              FILE1 and FILE2 have the same device and inode numbers

       FILE1 -nt FILE2
              FILE1 is newer (modification date) than FILE2

       FILE1 -ot FILE2
              FILE1 is older than FILE2

       -b FILE
              FILE exists and is block special

       -c FILE
              FILE exists and is character special

       -d FILE
              FILE exists and is a directory

       -e FILE
              FILE exists

       -f FILE
              FILE exists and is a regular file

       -g FILE
              FILE exists and is set-group-ID

       -G FILE
              FILE exists and is owned by the effective group ID

       -h FILE
              FILE exists and is a symbolic link (same as -L)

       -k FILE
              FILE exists and has its sticky bit set

       -L FILE
              FILE exists and is a symbolic link (same as -h)

       -O FILE
              FILE exists and is owned by the effective user ID

       -p FILE
              FILE exists and is a named pipe

       -r FILE
              FILE exists and read permission is granted

       -s FILE
              FILE exists and has a size greater than zero

       -S FILE
              FILE exists and is a socket

       -t FD  file descriptor FD is opened on a terminal

       -u FILE
              FILE exists and its set-user-ID bit is set

       -w FILE
              FILE exists and write permission is granted

       -x FILE
              FILE exists and execute (or search) permission is granted

       Except for -h and  -L,  all  FILE-related  tests  dereference  symbolic
       links.   Beware  that  parentheses  need  to be escaped (e.g., by back‐
       slashes) for shells.  INTEGER may also be -l STRING, which evaluates to
       the length of STRING.

       NOTE:  Binary  -a  and -o are inherently ambiguous.  Use 'test EXPR1 &&
       test EXPR2' or 'test EXPR1 || test EXPR2' instead.

       NOTE: [ honors the --help and --version options,  but  test  does  not.
       test treats each of those as it treats any other nonempty STRING.

       NOTE:  your shell may have its own version of test and/or [, which usu‐
       ally supersedes the version  described  here.   Please  refer  to  your
       shell's documentation for details about the options it supports.

AUTHOR
       Written by Kevin Braunsdorf and Matthew Bradburn.

REPORTING BUGS
       GNU coreutils online help: <https://www.gnu.org/software/coreutils/>
       Report [ translation bugs to <https://translationproject.org/team/>

COPYRIGHT
       Copyright  ©  2018  Free Software Foundation, Inc.  License GPLv3+: GNU
       GPL version 3 or later <https://gnu.org/licenses/gpl.html>.
       This is free software: you are free  to  change  and  redistribute  it.
       There is NO WARRANTY, to the extent permitted by law.

SEE ALSO
       Full documentation at: <https://www.gnu.org/software/coreutils/[>
       or available locally via: info '(coreutils) test invocation'

GNU coreutils 8.30              September 2019                         TEST(1)
BIND(2)                    Linux Programmer's Manual                   BIND(2)

NAME
       bind - bind a name to a socket

SYNOPSIS
       #include <sys/types.h>          /* See NOTES */
       #include <sys/socket.h>

       int bind(int sockfd, const struct sockaddr *addr,
                socklen_t addrlen);

DESCRIPTION
       When a socket is created with socket(2), it exists in a name space (ad‐
       dress family) but has no address assigned to it.   bind()  assigns  the
       address  specified  by  addr  to the socket referred to by the file de‐
       scriptor sockfd.  addrlen specifies the size, in bytes, of the  address
       structure  pointed to by addr.  Traditionally, this operation is called
       “assigning a name to a socket”.

       It is normally necessary to assign a local address using bind()  before
       a SOCK_STREAM socket may receive connections (see accept(2)).

       The  rules used in name binding vary between address families.  Consult
       the manual entries in Section 7 for detailed information.  For AF_INET,
       see  ip(7);  for  AF_INET6,  see ipv6(7); for AF_UNIX, see unix(7); for
       AF_APPLETALK, see ddp(7); for AF_PACKET, see packet(7); for AF_X25, see
       x25(7); and for AF_NETLINK, see netlink(7).

       The  actual  structure  passed for the addr argument will depend on the
       address family.  The sockaddr structure is defined as something like:

           struct sockaddr {
               sa_family_t sa_family;
               char        sa_data[14];
           }

       The only purpose of this structure is to  cast  the  structure  pointer
       passed in addr in order to avoid compiler warnings.  See EXAMPLE below.

RETURN VALUE
       On  success,  zero is returned.  On error, -1 is returned, and errno is
       set appropriately.

ERRORS
       EACCES The address is protected, and the user is not the superuser.

       EADDRINUSE
              The given address is already in use.

       EADDRINUSE
              (Internet domain sockets) The port number was specified as  zero
              in the socket address structure, but, upon attempting to bind to
              an ephemeral port, it was determined that all  port  numbers  in
              the  ephemeral port range are currently in use.  See the discus‐
              sion of /proc/sys/net/ipv4/ip_local_port_range ip(7).

       EBADF  sockfd is not a valid file descriptor.

       EINVAL The socket is already bound to an address.

       EINVAL addrlen is wrong, or addr  is  not  a  valid  address  for  this
              socket's domain.

       ENOTSOCK
              The file descriptor sockfd does not refer to a socket.

       The following errors are specific to UNIX domain (AF_UNIX) sockets:

       EACCES Search  permission  is denied on a component of the path prefix.
              (See also path_resolution(7).)

       EADDRNOTAVAIL
              A nonexistent interface was requested or the  requested  address
              was not local.

       EFAULT addr points outside the user's accessible address space.

       ELOOP  Too many symbolic links were encountered in resolving addr.

       ENAMETOOLONG
              addr is too long.

       ENOENT A  component in the directory prefix of the socket pathname does
              not exist.

       ENOMEM Insufficient kernel memory was available.

       ENOTDIR
              A component of the path prefix is not a directory.

       EROFS  The socket inode would reside on a read-only filesystem.

CONFORMING TO
       POSIX.1-2001, POSIX.1-2008, SVr4,  4.4BSD  (bind()  first  appeared  in
       4.2BSD).

NOTES
       POSIX.1  does  not  require  the  inclusion  of <sys/types.h>, and this
       header file is not required on Linux.  However, some  historical  (BSD)
       implementations  required  this  header file, and portable applications
       are probably wise to include it.

       For background on the socklen_t type, see accept(2).

BUGS
       The transparent proxy options are not described.

EXAMPLE
       An example of the use of bind() with Internet  domain  sockets  can  be
       found in getaddrinfo(3).

       The  following  example  shows  how to bind a stream socket in the UNIX
       (AF_UNIX) domain, and accept connections:

       #include <sys/socket.h>
       #include <sys/un.h>
       #include <stdlib.h>
       #include <stdio.h>
       #include <string.h>

       #define MY_SOCK_PATH "/somepath"
       #define LISTEN_BACKLOG 50

       #define handle_error(msg) \
           do { perror(msg); exit(EXIT_FAILURE); } while (0)

       int
       main(int argc, char *argv[])
       {
           int sfd, cfd;
           struct sockaddr_un my_addr, peer_addr;
           socklen_t peer_addr_size;

           sfd = socket(AF_UNIX, SOCK_STREAM, 0);
           if (sfd == -1)
               handle_error("socket");

           memset(&my_addr, 0, sizeof(struct sockaddr_un));
                               /* Clear structure */
           my_addr.sun_family = AF_UNIX;
           strncpy(my_addr.sun_path, MY_SOCK_PATH,
                   sizeof(my_addr.sun_path) - 1);

           if (bind(sfd, (struct sockaddr *) &my_addr,
                   sizeof(struct sockaddr_un)) == -1)
               handle_error("bind");

           if (listen(sfd, LISTEN_BACKLOG) == -1)
               handle_error("listen");

           /* Now we can accept incoming connections one
              at a time using accept(2) */

           peer_addr_size = sizeof(struct sockaddr_un);
           cfd = accept(sfd, (struct sockaddr *) &peer_addr,
                        &peer_addr_size);
           if (cfd == -1)
               handle_error("accept");

           /* Code to deal with incoming connection(s)... */

           /* When no longer required, the socket pathname, MY_SOCK_PATH
              should be deleted using unlink(2) or remove(3) */
       }

SEE ALSO
       accept(2), connect(2),  getsockname(2),  listen(2),  socket(2),  getad‐
       drinfo(3),    getifaddrs(3),    ip(7),   ipv6(7),   path_resolution(7),
       socket(7), unix(7)

COLOPHON
       This page is part of release 5.05 of the Linux  man-pages  project.   A
       description  of  the project, information about reporting bugs, and the
       latest    version    of    this    page,    can     be     found     at
       https://www.kernel.org/doc/man-pages/.

Linux                             2019-03-06                           BIND(2)
UNIMPLEMENTED(2)           Linux Programmer's Manual          UNIMPLEMENTED(2)

NAME
       afs_syscall,  break,  fattach,  fdetach,  ftime, getmsg, getpmsg, gtty,
       isastream, lock, madvise1, mpx, prof, profil,  putmsg,  putpmsg,  secu‐
       rity, stty, tuxcall, ulimit, vserver - unimplemented system calls

SYNOPSIS
       Unimplemented system calls.

DESCRIPTION
       These system calls are not implemented in the Linux kernel.

RETURN VALUE
       These system calls always return -1 and set errno to ENOSYS.

NOTES
       Note that ftime(3), profil(3), and ulimit(3) are implemented as library
       functions.

       Some system calls,  like  alloc_hugepages(2),  free_hugepages(2),  iop‐
       erm(2), iopl(2), and vm86(2) exist only on certain architectures.

       Some  system  calls, like ipc(2), create_module(2), init_module(2), and
       delete_module(2) exist only when the Linux kernel was built  with  sup‐
       port for them.

SEE ALSO
       syscalls(2)

COLOPHON
       This  page  is  part of release 5.05 of the Linux man-pages project.  A
       description of the project, information about reporting bugs,  and  the
       latest     version     of     this    page,    can    be    found    at
       https://www.kernel.org/doc/man-pages/.

Linux                             2017-09-15                  UNIMPLEMENTED(2)
DECLARE(7)               PostgreSQL 16.3 Documentation              DECLARE(7)

NAME
       DECLARE - define a cursor

SYNOPSIS
       DECLARE name [ BINARY ] [ ASENSITIVE | INSENSITIVE ] [ [ NO ] SCROLL ]
           CURSOR [ { WITH | WITHOUT } HOLD ] FOR query

DESCRIPTION
       DECLARE allows a user to create cursors, which can be used to retrieve
       a small number of rows at a time out of a larger query. After the
       cursor is created, rows are fetched from it using FETCH.

           Note
           This page describes usage of cursors at the SQL command level. If
           you are trying to use cursors inside a PL/pgSQL function, the rules
           are different — see Section 43.7.

PARAMETERS
       name
           The name of the cursor to be created. This must be different from
           any other active cursor name in the session.

       BINARY
           Causes the cursor to return data in binary rather than in text
           format.

       ASENSITIVE
       INSENSITIVE
           Cursor sensitivity determines whether changes to the data
           underlying the cursor, done in the same transaction, after the
           cursor has been declared, are visible in the cursor.  INSENSITIVE
           means they are not visible, ASENSITIVE means the behavior is
           implementation-dependent. A third behavior, SENSITIVE, meaning that
           such changes are visible in the cursor, is not available in
           PostgreSQL. In PostgreSQL, all cursors are insensitive; so these
           key words have no effect and are only accepted for compatibility
           with the SQL standard.

           Specifying INSENSITIVE together with FOR UPDATE or FOR SHARE is an
           error.

       SCROLL
       NO SCROLL
           SCROLL specifies that the cursor can be used to retrieve rows in a
           nonsequential fashion (e.g., backward). Depending upon the
           complexity of the query's execution plan, specifying SCROLL might
           impose a performance penalty on the query's execution time.  NO
           SCROLL specifies that the cursor cannot be used to retrieve rows in
           a nonsequential fashion. The default is to allow scrolling in some
           cases; this is not the same as specifying SCROLL. See Notes below
           for details.

       WITH HOLD
       WITHOUT HOLD
           WITH HOLD specifies that the cursor can continue to be used after
           the transaction that created it successfully commits.  WITHOUT HOLD
           specifies that the cursor cannot be used outside of the transaction
           that created it. If neither WITHOUT HOLD nor WITH HOLD is
           specified, WITHOUT HOLD is the default.

       query
           A SELECT or VALUES command which will provide the rows to be
           returned by the cursor.

       The key words ASENSITIVE, BINARY, INSENSITIVE, and SCROLL can appear in
       any order.

NOTES
       Normal cursors return data in text format, the same as a SELECT would
       produce. The BINARY option specifies that the cursor should return data
       in binary format. This reduces conversion effort for both the server
       and client, at the cost of more programmer effort to deal with
       platform-dependent binary data formats. As an example, if a query
       returns a value of one from an integer column, you would get a string
       of 1 with a default cursor, whereas with a binary cursor you would get
       a 4-byte field containing the internal representation of the value (in
       big-endian byte order).

       Binary cursors should be used carefully. Many applications, including
       psql, are not prepared to handle binary cursors and expect data to come
       back in the text format.

           Note
           When the client application uses the “extended query” protocol to
           issue a FETCH command, the Bind protocol message specifies whether
           data is to be retrieved in text or binary format. This choice
           overrides the way that the cursor is defined. The concept of a
           binary cursor as such is thus obsolete when using extended query
           protocol — any cursor can be treated as either text or binary.

       Unless WITH HOLD is specified, the cursor created by this command can
       only be used within the current transaction. Thus, DECLARE without WITH
       HOLD is useless outside a transaction block: the cursor would survive
       only to the completion of the statement. Therefore PostgreSQL reports
       an error if such a command is used outside a transaction block. Use
       BEGIN and COMMIT (or ROLLBACK) to define a transaction block.

       If WITH HOLD is specified and the transaction that created the cursor
       successfully commits, the cursor can continue to be accessed by
       subsequent transactions in the same session. (But if the creating
       transaction is aborted, the cursor is removed.) A cursor created with
       WITH HOLD is closed when an explicit CLOSE command is issued on it, or
       the session ends. In the current implementation, the rows represented
       by a held cursor are copied into a temporary file or memory area so
       that they remain available for subsequent transactions.

       WITH HOLD may not be specified when the query includes FOR UPDATE or
       FOR SHARE.

       The SCROLL option should be specified when defining a cursor that will
       be used to fetch backwards. This is required by the SQL standard.
       However, for compatibility with earlier versions, PostgreSQL will allow
       backward fetches without SCROLL, if the cursor's query plan is simple
       enough that no extra overhead is needed to support it. However,
       application developers are advised not to rely on using backward
       fetches from a cursor that has not been created with SCROLL. If NO
       SCROLL is specified, then backward fetches are disallowed in any case.

       Backward fetches are also disallowed when the query includes FOR UPDATE
       or FOR SHARE; therefore SCROLL may not be specified in this case.

           Caution
           Scrollable cursors may give unexpected results if they invoke any
           volatile functions (see Section 38.7). When a previously fetched
           row is re-fetched, the functions might be re-executed, perhaps
           leading to results different from the first time. It's best to
           specify NO SCROLL for a query involving volatile functions. If that
           is not practical, one workaround is to declare the cursor SCROLL
           WITH HOLD and commit the transaction before reading any rows from
           it. This will force the entire output of the cursor to be
           materialized in temporary storage, so that volatile functions are
           executed exactly once for each row.

       If the cursor's query includes FOR UPDATE or FOR SHARE, then returned
       rows are locked at the time they are first fetched, in the same way as
       for a regular SELECT command with these options. In addition, the
       returned rows will be the most up-to-date versions.

           Caution
           It is generally recommended to use FOR UPDATE if the cursor is
           intended to be used with UPDATE ... WHERE CURRENT OF or DELETE ...
           WHERE CURRENT OF. Using FOR UPDATE prevents other sessions from
           changing the rows between the time they are fetched and the time
           they are updated. Without FOR UPDATE, a subsequent WHERE CURRENT OF
           command will have no effect if the row was changed since the cursor
           was created.

           Another reason to use FOR UPDATE is that without it, a subsequent
           WHERE CURRENT OF might fail if the cursor query does not meet the
           SQL standard's rules for being “simply updatable” (in particular,
           the cursor must reference just one table and not use grouping or
           ORDER BY). Cursors that are not simply updatable might work, or
           might not, depending on plan choice details; so in the worst case,
           an application might work in testing and then fail in production.
           If FOR UPDATE is specified, the cursor is guaranteed to be
           updatable.

           The main reason not to use FOR UPDATE with WHERE CURRENT OF is if
           you need the cursor to be scrollable, or to be isolated from
           concurrent updates (that is, continue to show the old data). If
           this is a requirement, pay close heed to the caveats shown above.

       The SQL standard only makes provisions for cursors in embedded SQL. The
       PostgreSQL server does not implement an OPEN statement for cursors; a
       cursor is considered to be open when it is declared. However, ECPG, the
       embedded SQL preprocessor for PostgreSQL, supports the standard SQL
       cursor conventions, including those involving DECLARE and OPEN
       statements.

       The server data structure underlying an open cursor is called a portal.
       Portal names are exposed in the client protocol: a client can fetch
       rows directly from an open portal, if it knows the portal name. When
       creating a cursor with DECLARE, the portal name is the same as the
       cursor name.

       You can see all available cursors by querying the pg_cursors system
       view.

EXAMPLES
       To declare a cursor:

           DECLARE liahona CURSOR FOR SELECT * FROM films;

       See FETCH(7) for more examples of cursor usage.

COMPATIBILITY
       The SQL standard allows cursors only in embedded SQL and in modules.
       PostgreSQL permits cursors to be used interactively.

       According to the SQL standard, changes made to insensitive cursors by
       UPDATE ... WHERE CURRENT OF and DELETE ... WHERE CURRENT OF statements
       are visible in that same cursor.  PostgreSQL treats these statements
       like all other data changing statements in that they are not visible in
       insensitive cursors.

       Binary cursors are a PostgreSQL extension.

SEE ALSO
       CLOSE(7), FETCH(7), MOVE(7)

PostgreSQL 16.3                      2024                           DECLARE(7)
ECHO(1)                          User Commands                         ECHO(1)

NAME
       echo - display a line of text

SYNOPSIS
       echo [SHORT-OPTION]... [STRING]...
       echo LONG-OPTION

DESCRIPTION
       Echo the STRING(s) to standard output.

       -n     do not output the trailing newline

       -e     enable interpretation of backslash escapes

       -E     disable interpretation of backslash escapes (default)

       --help display this help and exit

       --version
              output version information and exit

       If -e is in effect, the following sequences are recognized:

       \\     backslash

       \a     alert (BEL)

       \b     backspace

       \c     produce no further output

       \e     escape

       \f     form feed

       \n     new line

       \r     carriage return

       \t     horizontal tab

       \v     vertical tab

       \0NNN  byte with octal value NNN (1 to 3 digits)

       \xHH   byte with hexadecimal value HH (1 to 2 digits)

       NOTE: your shell may have its own version of echo, which usually super‐
       sedes the version described here.  Please refer to your  shell's  docu‐
       mentation for details about the options it supports.

AUTHOR
       Written by Brian Fox and Chet Ramey.

REPORTING BUGS
       GNU coreutils online help: <https://www.gnu.org/software/coreutils/>
       Report echo translation bugs to <https://translationproject.org/team/>

COPYRIGHT
       Copyright  ©  2018  Free Software Foundation, Inc.  License GPLv3+: GNU
       GPL version 3 or later <https://gnu.org/licenses/gpl.html>.
       This is free software: you are free  to  change  and  redistribute  it.
       There is NO WARRANTY, to the extent permitted by law.

SEE ALSO
       Full documentation at: <https://www.gnu.org/software/coreutils/echo>
       or available locally via: info '(coreutils) echo invocation'

GNU coreutils 8.30              September 2019                         ECHO(1)
EXEC(3)                    Linux Programmer's Manual                   EXEC(3)

NAME
       execl, execlp, execle, execv, execvp, execvpe - execute a file

SYNOPSIS
       #include <unistd.h>

       extern char **environ;

       int execl(const char *pathname, const char *arg, ...
                       /* (char  *) NULL */);
       int execlp(const char *file, const char *arg, ...
                       /* (char  *) NULL */);
       int execle(const char *pathname, const char *arg, ...
                       /*, (char *) NULL, char *const envp[] */);
       int execv(const char *pathname, char *const argv[]);
       int execvp(const char *file, char *const argv[]);
       int execvpe(const char *file, char *const argv[],
                       char *const envp[]);

   Feature Test Macro Requirements for glibc (see feature_test_macros(7)):

       execvpe(): _GNU_SOURCE

DESCRIPTION
       The  exec() family of functions replaces the current process image with
       a new process image.  The functions described in this manual  page  are
       front-ends  for execve(2).  (See the manual page for execve(2) for fur‐
       ther details about the replacement of the current process image.)

       The initial argument for these functions is the name of a file that  is
       to be executed.

       The  functions can be grouped based on the letters following the "exec"
       prefix.

   l - execl(), execlp(), execle()
       The const char *arg and subsequent ellipses can be thought of as  arg0,
       arg1, ..., argn.  Together they describe a list of one or more pointers
       to null-terminated strings that represent the argument  list  available
       to  the  executed  program.   The first argument, by convention, should
       point to the filename associated with the  file  being  executed.   The
       list  of  arguments  must  be  terminated by a null pointer, and, since
       these are variadic functions, this pointer must be cast (char *) NULL.

       By contrast with the 'l' functions, the 'v' functions  (below)  specify
       the command-line arguments of the executed program as a vector.

   v - execv(), execvp(), execvpe()
       The  char *const argv[] argument is an array of pointers to null-termi‐
       nated strings that represent the argument list  available  to  the  new
       program.   The first argument, by convention, should point to the file‐
       name associated with the file being executed.  The  array  of  pointers
       must be terminated by a null pointer.

   e - execle(), execvpe()
       The  environment of the caller is specified via the argument envp.  The
       envp argument is an array of pointers to  null-terminated  strings  and
       must be terminated by a null pointer.

       All  other  exec()  functions  (which do not include 'e' in the suffix)
       take the environment for the new process image from the external  vari‐
       able environ in the calling process.

   p - execlp(), execvp(), execvpe()
       These  functions duplicate the actions of the shell in searching for an
       executable file if the specified filename does not contain a slash  (/)
       character.  The file is sought in the colon-separated list of directory
       pathnames specified in the PATH environment variable.  If this variable
       isn't  defined,  the path list defaults to a list that includes the di‐
       rectories returned by confstr(_CS_PATH) (which  typically  returns  the
       value "/bin:/usr/bin") and possibly also the current working directory;
       see NOTES for further details.

       If the specified filename includes a slash character, then PATH is  ig‐
       nored, and the file at the specified pathname is executed.

       In addition, certain errors are treated specially.

       If permission is denied for a file (the attempted execve(2) failed with
       the error EACCES), these functions will continue searching the rest  of
       the  search path.  If no other file is found, however, they will return
       with errno set to EACCES.

       If the header of a  file  isn't  recognized  (the  attempted  execve(2)
       failed  with the error ENOEXEC), these functions will execute the shell
       (/bin/sh) with the path of the file as its first  argument.   (If  this
       attempt fails, no further searching is done.)

       All  other  exec()  functions  (which do not include 'p' in the suffix)
       take as their first argument a (relative  or  absolute)  pathname  that
       identifies the program to be executed.

RETURN VALUE
       The  exec() functions return only if an error has occurred.  The return
       value is -1, and errno is set to indicate the error.

ERRORS
       All of these functions may fail and set errno for  any  of  the  errors
       specified for execve(2).

VERSIONS
       The execvpe() function first appeared in glibc 2.11.

ATTRIBUTES
       For  an  explanation  of  the  terms  used  in  this  section,  see at‐
       tributes(7).

       ┌──────────────────────────────┬───────────────┬─────────────┐
       │Interface                     │ Attribute     │ Value       │
       ├──────────────────────────────┼───────────────┼─────────────┤
       │execl(), execle(), execv()    │ Thread safety │ MT-Safe     │
       ├──────────────────────────────┼───────────────┼─────────────┤
       │execlp(), execvp(), execvpe() │ Thread safety │ MT-Safe env │
       └──────────────────────────────┴───────────────┴─────────────┘
CONFORMING TO
       POSIX.1-2001, POSIX.1-2008.

       The execvpe() function is a GNU extension.

NOTES
       The default search path (used when the environment does not contain the
       variable  PATH)  shows some variation across systems.  It generally in‐
       cludes /bin and /usr/bin (in that order) and may also include the  cur‐
       rent  working directory.  On some other systems, the current working is
       included after /bin and /usr/bin, as an anti-Trojan-horse measure.  The
       glibc  implementation  long  followed the traditional default where the
       current working directory is included at the start of the search  path.
       However,  some  code  refactoring  during the development of glibc 2.24
       caused the current working directory to be dropped altogether from  the
       default  search  path.   This  accidental behavior change is considered
       mildly beneficial, and won't be reverted.

       The behavior of execlp() and execvp() when errors occur while  attempt‐
       ing to execute the file is historic practice, but has not traditionally
       been documented and is not specified by the POSIX standard.   BSD  (and
       possibly  other  systems) do an automatic sleep and retry if ETXTBSY is
       encountered.  Linux treats it as a hard error and returns immediately.

       Traditionally, the functions execlp() and execvp() ignored  all  errors
       except  for  the  ones described above and ENOMEM and E2BIG, upon which
       they returned.  They now return if any error other than  the  ones  de‐
       scribed above occurs.

BUGS
       Before  glibc 2.24, execl() and execle() employed realloc(3) internally
       and were consequently not async-signal-safe, in violation  of  the  re‐
       quirements of POSIX.1.  This was fixed in glibc 2.24.

   Architecture-specific details
       On  sparc and sparc64, execv() is provided as a system call by the ker‐
       nel (with the prototype shown  above)  for  compatibility  with  SunOS.
       This  function is not employed by the execv() wrapper function on those
       architectures.

SEE ALSO
       sh(1), execve(2), execveat(2),  fork(2),  ptrace(2),  fexecve(3),  sys‐
       tem(3), environ(7)

COLOPHON
       This  page  is  part of release 5.05 of the Linux man-pages project.  A
       description of the project, information about reporting bugs,  and  the
       latest     version     of     this    page,    can    be    found    at
       https://www.kernel.org/doc/man-pages/.

GNU                               2019-08-02                           EXEC(3)
EXIT(3)                    Linux Programmer's Manual                   EXIT(3)

NAME
       exit - cause normal process termination

SYNOPSIS
       #include <stdlib.h>

       void exit(int status);

DESCRIPTION
       The  exit() function causes normal process termination and the value of
       status & 0xFF is returned to the parent (see wait(2)).

       All functions registered with atexit(3) and on_exit(3) are  called,  in
       the  reverse  order  of their registration.  (It is possible for one of
       these functions to use atexit(3) or on_exit(3)  to  register  an  addi‐
       tional  function  to be executed during exit processing; the new regis‐
       tration is added to the front of the list of functions that  remain  to
       be  called.)  If one of these functions does not return (e.g., it calls
       _exit(2), or kills itself with a signal), then none  of  the  remaining
       functions is called, and further exit processing (in particular, flush‐
       ing of stdio(3) streams) is abandoned.  If a function has  been  regis‐
       tered  multiple  times using atexit(3) or on_exit(3), then it is called
       as many times as it was registered.

       All open stdio(3) streams are flushed and  closed.   Files  created  by
       tmpfile(3) are removed.

       The  C standard specifies two constants, EXIT_SUCCESS and EXIT_FAILURE,
       that may be passed to exit() to  indicate  successful  or  unsuccessful
       termination, respectively.

RETURN VALUE
       The exit() function does not return.

ATTRIBUTES
       For  an  explanation  of  the  terms  used  in  this  section,  see at‐
       tributes(7).

       ┌──────────┬───────────────┬─────────────────────┐
       │Interface │ Attribute     │ Value               │
       ├──────────┼───────────────┼─────────────────────┤
       │exit()    │ Thread safety │ MT-Unsafe race:exit │
       └──────────┴───────────────┴─────────────────────┘
       The exit() function uses a global variable that is not protected, so it
       is not thread-safe.

CONFORMING TO
       POSIX.1-2001, POSIX.1-2008, C89, C99, SVr4, 4.3BSD.

NOTES
       The  behavior  is  undefined  if  one of the functions registered using
       atexit(3) and on_exit(3) calls either exit() or longjmp(3).  Note  that
       a  call  to execve(2) removes registrations created using atexit(3) and
       on_exit(3).

       The use of EXIT_SUCCESS and EXIT_FAILURE is slightly more portable  (to
       non-UNIX  environments) than the use of 0 and some nonzero value like 1
       or -1.  In particular, VMS uses a different convention.

       BSD has attempted to standardize exit codes  (which  some  C  libraries
       such  as  the  GNU  C  library have also adopted); see the file <sysex‐
       its.h>.

       After exit(), the  exit  status  must  be  transmitted  to  the  parent
       process.  There are three cases:

       •  If  the  parent has set SA_NOCLDWAIT, or has set the SIGCHLD handler
          to SIG_IGN, the status is discarded and the child dies immediately.

       •  If the parent was waiting on the child, it is notified of  the  exit
          status and the child dies immediately.

       •  Otherwise, the child becomes a "zombie" process: most of the process
          resources are recycled, but a slot  containing  minimal  information
          about  the child process (termination status, resource usage statis‐
          tics) is retained in process table.  This allows the parent to  sub‐
          sequently  use waitpid(2) (or similar) to learn the termination sta‐
          tus of the child; at that point the zombie process slot is released.

       If the implementation supports the SIGCHLD signal, this signal is  sent
       to  the  parent.   If  the parent has set SA_NOCLDWAIT, it is undefined
       whether a SIGCHLD signal is sent.

   Signals sent to other processes
       If the exiting process is a session leader and its controlling terminal
       is  the  controlling  terminal of the session, then each process in the
       foreground process group of this controlling terminal is sent a  SIGHUP
       signal,  and  the terminal is disassociated from this session, allowing
       it to be acquired by a new controlling process.

       If the exit of the process causes a process group to  become  orphaned,
       and  if any member of the newly orphaned process group is stopped, then
       a SIGHUP signal followed by a SIGCONT  signal  will  be  sent  to  each
       process  in  this  process group.  See setpgid(2) for an explanation of
       orphaned process groups.

       Except in the above cases, where the signalled processes may  be  chil‐
       dren  of  the terminating process, termination of a process does not in
       general cause a signal to be sent to children of  that  process.   How‐
       ever,  a process can use the prctl(2) PR_SET_PDEATHSIG operation to ar‐
       range that it receives a signal if its parent terminates.

SEE ALSO
       _exit(2),   get_robust_list(2),   setpgid(2),    wait(2),    atexit(3),
       on_exit(3), tmpfile(3)

COLOPHON
       This  page  is  part of release 5.05 of the Linux man-pages project.  A
       description of the project, information about reporting bugs,  and  the
       latest     version     of     this    page,    can    be    found    at
       https://www.kernel.org/doc/man-pages/.

Linux                             2020-02-09                           EXIT(3)
FALSE(1)                         User Commands                        FALSE(1)

NAME
       false - do nothing, unsuccessfully

SYNOPSIS
       false [ignored command line arguments]
       false OPTION

DESCRIPTION
       Exit with a status code indicating failure.

       --help display this help and exit

       --version
              output version information and exit

       NOTE:  your  shell may have its own version of false, which usually su‐
       persedes the version described here.  Please refer to your shell's doc‐
       umentation for details about the options it supports.

AUTHOR
       Written by Jim Meyering.

REPORTING BUGS
       GNU coreutils online help: <https://www.gnu.org/software/coreutils/>
       Report false translation bugs to <https://translationproject.org/team/>

COPYRIGHT
       Copyright  ©  2018  Free Software Foundation, Inc.  License GPLv3+: GNU
       GPL version 3 or later <https://gnu.org/licenses/gpl.html>.
       This is free software: you are free  to  change  and  redistribute  it.
       There is NO WARRANTY, to the extent permitted by law.

SEE ALSO
       Full documentation at: <https://www.gnu.org/software/coreutils/false>
       or available locally via: info '(coreutils) false invocation'

GNU coreutils 8.30              September 2019                        FALSE(1)
HASH(3)                    Linux Programmer's Manual                   HASH(3)

NAME
       hash - hash database access method

SYNOPSIS
       #include <sys/types.h>
       #include <db.h>

DESCRIPTION
       Note  well:  This  page documents interfaces provided in glibc up until
       version 2.1.  Since version 2.2, glibc no longer provides these  inter‐
       faces.   Probably,  you  are looking for the APIs provided by the libdb
       library instead.

       The routine dbopen(3) is the library interface to database files.   One
       of  the  supported file formats is hash files.  The general description
       of the database access methods is in dbopen(3), this  manual  page  de‐
       scribes only the hash-specific information.

       The hash data structure is an extensible, dynamic hashing scheme.

       The  access-method-specific data structure provided to dbopen(3) is de‐
       fined in the <db.h> include file as follows:

           typedef struct {
               unsigned int       bsize;
               unsigned int       ffactor;
               unsigned int       nelem;
               unsigned int       cachesize;
               uint32_t         (*hash)(const void *, size_t);
               int         lorder;
           } HASHINFO;

       The elements of this structure are as follows:

       bsize     defines the hash table bucket size, and is, by  default,  256
                 bytes.   It  may  be preferable to increase the page size for
                 disk-resident tables and tables with large data items.

       ffactor   indicates a desired density within the hash table.  It is  an
                 approximation  of the number of keys allowed to accumulate in
                 any one bucket, determining when  the  hash  table  grows  or
                 shrinks.  The default value is 8.

       nelem     is  an  estimate of the final size of the hash table.  If not
                 set or set too low, hash tables  will  expand  gracefully  as
                 keys  are  entered, although a slight performance degradation
                 may be noticed.  The default value is 1.

       cachesize is the suggested maximum size, in bytes, of the memory cache.
                 This value is only advisory, and the access method will allo‐
                 cate more memory rather than fail.

       hash      is a user-defined hash function.  Since no hash function per‐
                 forms  equally  well  on all possible data, the user may find
                 that the built-in hash function does poorly on  a  particular
                 data  set.  A user-specified hash functions must take two ar‐
                 guments (a pointer to a byte string and a length) and  return
                 a 32-bit quantity to be used as the hash value.

       lorder    is  the  byte order for integers in the stored database meta‐
                 data.  The number should represent the order as  an  integer;
                 for  example, big endian order would be the number 4,321.  If
                 lorder is 0 (no order is specified), the current  host  order
                 is  used.  If the file already exists, the specified value is
                 ignored and the value specified when the tree was created  is
                 used.

       If the file already exists (and the O_TRUNC flag is not specified), the
       values specified for bsize, ffactor, lorder, and nelem are ignored  and
       the values specified when the tree was created are used.

       If a hash function is specified, hash_open attempts to determine if the
       hash function specified is the same as the one with which the  database
       was created, and fails if it is not.

       Backward-compatible interfaces to the routines described in dbm(3), and
       ndbm(3) are provided, however these interfaces are not compatible  with
       previous file formats.

ERRORS
       The  hash  access method routines may fail and set errno for any of the
       errors specified for the library routine dbopen(3).

BUGS
       Only big and little endian byte order are supported.

SEE ALSO
       btree(3), dbopen(3), mpool(3), recno(3)

       Dynamic Hash Tables, Per-Ake Larson, Communications of the  ACM,  April
       1988.

       A  New Hash Package for UNIX, Margo Seltzer, USENIX Proceedings, Winter
       1991.

COLOPHON
       This page is part of release 5.05 of the Linux  man-pages  project.   A
       description  of  the project, information about reporting bugs, and the
       latest    version    of    this    page,    can     be     found     at
       https://www.kernel.org/doc/man-pages/.

4.4 Berkeley Distribution         2017-09-15                           HASH(3)
HISTORY(3)                 Library Functions Manual                 HISTORY(3)

NAME
       history - GNU History Library

COPYRIGHT
       The GNU History Library is Copyright (C) 1989-2017 by the Free Software
       Foundation, Inc.

DESCRIPTION
       Many programs read input from the user a line at a time.  The GNU  His‐
       tory  library is able to keep track of those lines, associate arbitrary
       data with each line, and utilize information  from  previous  lines  in
       composing new ones.

HISTORY EXPANSION
       The  history library supports a history expansion feature that is iden‐
       tical to the history expansion in bash.  This  section  describes  what
       syntax features are available.

       History expansions introduce words from the history list into the input
       stream, making it easy to repeat commands, insert the  arguments  to  a
       previous command into the current input line, or fix errors in previous
       commands quickly.

       History expansion is usually performed  immediately  after  a  complete
       line  is read.  It takes place in two parts.  The first is to determine
       which line from the history list to use during substitution.  The  sec‐
       ond  is  to select portions of that line for inclusion into the current
       one.  The line selected from the history is the event, and the portions
       of  that  line  that  are  acted upon are words.  Various modifiers are
       available to manipulate the selected words.  The line  is  broken  into
       words in the same fashion as bash does when reading input, so that sev‐
       eral words that would otherwise be separated are  considered  one  word
       when  surrounded  by  quotes (see the description of history_tokenize()
       below).  History expansions are introduced by  the  appearance  of  the
       history expansion character, which is ! by default.  Only backslash (\)
       and single quotes can quote the history expansion character.

   Event Designators
       An event designator is a reference to a command line entry in the  his‐
       tory  list.   Unless  the reference is absolute, events are relative to
       the current position in the history list.

       !      Start a history substitution, except when followed by  a  blank,
              newline, = or (.
       !n     Refer to command line n.
       !-n    Refer to the current command minus n.
       !!     Refer to the previous command.  This is a synonym for `!-1'.
       !string
              Refer  to the most recent command preceding the current position
              in the history list starting with string.
       !?string[?]
              Refer to the most recent command preceding the current  position
              in  the  history  list containing string.  The trailing ? may be
              omitted if string is followed immediately by a newline.
       ^string1^string2^
              Quick substitution.  Repeat the last command, replacing  string1
              with string2.  Equivalent to ``!!:s/string1/string2/'' (see Mod‐
              ifiers below).
       !#     The entire command line typed so far.

   Word Designators
       Word designators are used to select desired words from the event.  A  :
       separates  the event specification from the word designator.  It may be
       omitted if the word designator begins with a ^, $, *, -, or  %.   Words
       are  numbered from the beginning of the line, with the first word being
       denoted by 0 (zero).  Words are inserted into the  current  line  sepa‐
       rated by single spaces.

       0 (zero)
              The zeroth word.  For the shell, this is the command word.
       n      The nth word.
       ^      The first argument.  That is, word 1.
       $      The  last word.  This is usually the last argument, but will ex‐
              pand to the zeroth word if there is only one word in the line.
       %      The word matched by the most recent `?string?' search.
       x-y    A range of words; `-y' abbreviates `0-y'.
       *      All of the words but the zeroth.  This is a synonym  for  `1-$'.
              It  is  not  an  error to use * if there is just one word in the
              event; the empty string is returned in that case.
       x*     Abbreviates x-$.
       x-     Abbreviates x-$ like x*, but omits the last word.

       If a word designator is supplied without an  event  specification,  the
       previous command is used as the event.

   Modifiers
       After  the optional word designator, there may appear a sequence of one
       or more of the following modifiers, each preceded by a `:'.

       h      Remove a trailing file name component, leaving only the head.
       t      Remove all leading file name components, leaving the tail.
       r      Remove a trailing suffix of the form .xxx, leaving the basename.
       e      Remove all but the trailing suffix.
       p      Print the new command but do not execute it.
       q      Quote the substituted words, escaping further substitutions.
       x      Quote the substituted words as with q, but break into  words  at
              blanks and newlines.
       s/old/new/
              Substitute  new  for  the  first  occurrence of old in the event
              line.  Any delimiter can be used in place of /.  The  final  de‐
              limiter  is  optional  if  it is the last character of the event
              line.  The delimiter may be quoted in old and new with a  single
              backslash.   If & appears in new, it is replaced by old.  A sin‐
              gle backslash will quote the &.  If old is null, it  is  set  to
              the  last  old substituted, or, if no previous history substitu‐
              tions took place, the last string in a !?string[?]  search.
       &      Repeat the previous substitution.
       g      Cause changes to be applied over the entire event line.  This is
              used  in  conjunction  with `:s' (e.g., `:gs/old/new/') or `:&'.
              If used with `:s', any delimiter can be used in place of /,  and
              the  final  delimiter is optional if it is the last character of
              the event line.  An a may be used as a synonym for g.
       G      Apply the following `s' modifier once to each word in the  event
              line.

PROGRAMMING WITH HISTORY FUNCTIONS
       This  section  describes  how  to use the History library in other pro‐
       grams.

   Introduction to History
       The programmer using the History library has  available  functions  for
       remembering  lines on a history list, associating arbitrary data with a
       line, removing lines from the list, searching through the  list  for  a
       line  containing  an arbitrary text string, and referencing any line in
       the list directly.  In addition, a history expansion function is avail‐
       able  which  provides  for a consistent user interface across different
       programs.

       The user using programs written with the History library has the  bene‐
       fit  of  a  consistent user interface with a set of well-known commands
       for manipulating the text of previous lines and using that text in  new
       commands.  The basic history manipulation commands are identical to the
