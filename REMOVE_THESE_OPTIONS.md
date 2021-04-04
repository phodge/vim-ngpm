Indent/Formatting extension:
	'autoindent'	  'ai'	    take indent for new line from previous line
	'cindent'	  'cin'     do C program indenting
	'cinkeys'	  'cink'    keys that trigger indent when 'cindent' is set
	'cinoptions'	  'cino'    how to do indenting when 'cindent' is set
	'cinwords'	  'cinw'    words where 'si' and 'cin' add an indent
	'comments'	  'com'     patterns that can start a comment line
	'commentstring'   'cms'     template for comments; used for fold marker
	'copyindent'	  'ci'	    make 'autoindent' use existing indent structure
	'equalprg'	  'ep'	    external program to use for "=" command
	'formatexpr'	  'fex'     expression used with "gq" command
	'formatlistpat'   'flp'     pattern used to recognize a list header
	'formatoptions'   'fo'	    how automatic formatting is to be done
	'formatprg'	  'fp'	    name of external program used with "gq" command
	'indentexpr'	  'inde'    expression used to obtain the indent of a line
	'indentkeys'	  'indk'    keys that trigger indenting with 'indentexpr'
	'lisp'			    automatic indenting for Lisp
	'lispwords'	  'lw'	    words that change how lisp indenting works
	'preserveindent'  'pi'	    preserve the indent structure when reindenting
	'smartindent'	  'si'	    smart autoindenting for C programs
	'textwidth'	  'tw'	    maximum width of text that is being inserted

Completion extensions:
	'complete'	  'cpt'     specify how Insert mode completion works
	'completefunc'	  'cfu'     function to be used for Insert mode completion
	'completeopt'	  'cot'     options for Insert mode completion
	'dictionary'	  'dict'    list of file names used for keyword completion
	'infercase'	  'inf'     adjust case of match for keyword completion
	'omnifunc'	  'ofu'     function for filetype-specific completion
	'showfulltag'	  'sft'     show full tag pattern when completing tag
	'thesaurus'	  'tsr'     list of thesaurus files for keyword completion

CScope extension:
	'cscopepathcomp'  'cspc'    how many components of the path to show
	'cscopeprg'       'csprg'   command to execute cscope
	'cscopequickfix'  'csqf'    use quickfix window for cscope results
	'cscoperelative'  'csre'    Use cscope.out path basename as prefix
	'cscopetag'       'cst'     use cscope for tag commands
	'cscopetagorder'  'csto'    determines ":cstag" search order
	'cscopeverbose'   'csverb'  give messages when adding a cscope database

Code navigation extension:
	'define'	  'def'     pattern to be used to find a macro definition
	'include'	  'inc'     pattern to be used to find an include file
	'includeexpr'	  'inex'    expression used to process an include line

Ctags extension:
	'tagbsearch'	  'tbs'     use binary searching in tags files
	'tagcase'	  'tc'      how to handle case when searching in tags files
	'taglength'	  'tl'	    number of significant characters for a tag
	'tagrelative'	  'tr'	    file names in tag file are relative
	'tags'		  'tag'     list of file names used by the tag command
	'tagstack'	  'tgst'    push tags onto the tag stack

Plugins for :make, :grep, :vimgrep, etc:
	'grepformat'	  'gfm'     format of 'grepprg' output
	'grepprg'	  'gp'	    program to use for ":grep"
	'makeef'	  'mef'     name of the errorfile for ":make"
	'makeencoding'	  'menc'    encoding of external make/grep commands
	'makeprg'	  'mp'	    program to use for the ":make" command
	'shellpipe'	  'sp'	    string to put output of ":make" in error file

A "%" match-jumping extension:
	'matchpairs'	  'mps'     pairs of characters that "%" can match
	'matchtime'	  'mat'     tenths of a second to show matching paren
	'showmatch'	  'sm'	    briefly jump to matching bracket if insert one

If line numbers could be implemented via custom signcolumns:
	'number'	  'nu'	    print the line number in front of each line
	'numberwidth'	  'nuw'     number of columns used for the line number
	'relativenumber'  'rnu'	    show relative line number in front of each line

A spelling extension:
	'mkspellmem'	  'msm'     memory used before |:mkspell| compresses the tree
	'spell'			    enable spell checking
	'spellcapcheck'   'spc'     pattern to locate end of a sentence
	'spellfile'	  'spf'     files where |zg| and |zw| store words
	'spelllang'	  'spl'     language(s) to do spell checking for
	'spellsuggest'	  'sps'     method(s) used to suggest spelling corrections

Statusline extension:
	'ruler'		  'ru'	    show cursor line and column in the status line
	'rulerformat'	  'ruf'     custom format for the ruler
	'statusline'	  'stl'     custom format for the status line

Help functionality could be moved into an extension:
	'helpfile'	  'hf'	    full path name of the main help file
	'helpheight'	  'hh'	    minimum height of a new help window
	'helplang'	  'hlg'     preferred help languages
	'keywordprg'	  'kp'	    program to use for the "K" command

Backup extension:
	'backup'	  'bk'	    keep backup file after overwriting a file
	'backupcopy'	  'bkc'     make backup as a copy, don't rename the file
	'backupdir'	  'bdir'    list of directories for the backup file
	'backupskip'	  'bsk'     no backup for files that match these patterns
	'backupext'	  'bex'     extension used for the backup file
	'patchmode'	  'pm'	    keep the oldest version of a file
	'writebackup'	  'wb'	    make a backup before overwriting a file

Packages as an extension:
	'packpath'	  'pp'      list of directories used for packages

If custom motions were possible via extensions:
	'paragraphs'	  'para'    nroff macros that separate paragraphs
	'quoteescape'	  'qe'	    escape characters used in a string

Other:
	'insertmode'	  'im'	    start the edit of a file in Insert mode
	'regexpengine'	  're'	    default regexp engine to use
	'tildeop'	  'top'     tilde command "~" behaves like an operator
	'viewdir'	  'vdir'    directory where to store files with :mkview
	'viewoptions'	  'vop'     specifies what to save for :mkview
	'autochdir'	  'acd'     change directory to the file in the current window
	'nrformats'	  'nf'	    number formats recognized for CTRL-A command
