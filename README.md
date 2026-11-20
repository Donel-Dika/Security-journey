# Security-journey
Day 1 -  19/11/2026 Goal: AI security
Today: GitHub set up, starting OverTheWire Bandit

19/11 – Bandit level 2 reached.
- Level 1→2: "-" means stdin for most commands; use ./- to refer to a file named "-".
- SSH format: user@server -p 2220 (dot vs @ mistake cost me 2 min).

20/11 – Level 2→3:
- filenames with spaces → escape with "\ " or use quotes; Tab autocomplete does it automatically.
-  A trailing \ means "line continues."

20/11 – Level 3→4: 
- hidden files start with "." → ls -a shows them; options combine (-la). 
- Permissions: -rw-r----- = owner rw, group r, others nothing. Group membership decides access.

 20/11 – Level 5→6: find (hardest level so far)

### Structure
find <where> <condition> <condition> ...
- where: . = current folder + ALL subfolders (recursive)
- conditions are combined with AND by default

### Most useful conditions
- -type f        → only files (d = only directories)
- -name "x*"     → by name, wildcards allowed (use quotes)
- -size 1033c    → exact size in BYTES (c = bytes!)
    - +1000c = bigger than, -1000c = smaller than
    - b = 512-byte blocks (default!), k = KB, M = MB, G = GB
- -readable      → I can read it
- -executable    → it can be executed
- ! <condition>  → NOT (e.g. ! -executable)
- -user bandit7 / -group bandit6 → by owner/group

### Combining with other commands
- -exec file {} +       → run 'file' on every result ({} = the result)
- | grep text           → pipe: send output to grep, keep matching lines
- 2>/dev/null           → hide error messages (e.g. "Permission denied")

### Full solution pattern
find . -type f -size 1033c ! -executable -exec file {} + | grep text

### Lessons
- read the level conditions → translate each one into a find option
- size without a unit letter is NOT bytes
- find gives full paths → cat ./folder/.file (folder/file)
- ./ only needed for names starting with "-" or to run scripts

