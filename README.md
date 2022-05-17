# Command Line Flags Library

## Features

 - Minimalistic design
 - Minimum third-party dependencies
 - Cross-platform (`gcc`, `mingw`, `msvc`)
 - Header only
 - Thread-safe
 - Simple integration (`cmake`)
 - Project name and version are available.

## How to use

Define required command line parameter variables

```c++
/* Define command line flags
 */
Flags OPT_BOOL("opt1", false);

/* Define command line flags
 * with explicit type specification
 */
Flags<int> OPT_WITH_TYPE("opt2", 0);

/* Define command line flags
 * with description
 */
Flags OPT_WITH_DESC("opt3", 0U, 
    "Option #2 with description");

/* Define command line flags
 * with validator
 */
Flags OPT_WITH_VALIDATOR("opt4", 0U, 
    [](auto v) { return v < 7U; });
```

Implement the variable defined in one file to access another file

```c++
/* Implement special flags
 */ 
DECLARE_string(PROGECT_NAME);
DECLARE_string(PROGECT_VERSION);

/* Implement variable defined
 * in another file
 */ 
DECLARE_bool(OPT_BOOL);
```

Process command line flags and set their values according to input parameters

```c++
#include <iostream>
#include "flags.h"

int main(int argc, char* argv[]) {

    /* Parsing command line parameters 
    */
    try {
        IFlags::parse(argc, argv);
    } catch (const std::exception& e) {
        std::cout << e.what();
    }
    
    /* Changing the flag value
     */   
    OPT_BOOL = true;
    OPT_WITH_DESC = 1;
    
    /* Get flag value
     */
    std::cerr 
      << "\nNAME: " << PROGECT_NAME() 
      << "\nVERSION: " << PROGECT_VERSION()
      << "\nOPTION1: " << OPT_BOOL()
      << "\nOPTION2: " << OPT_WITH_TYPE()
      << "\nOPTION3: " << OPT_WITH_DESC()
      << "\nOPTION4: " << OPT_WITH_VALIDATOR()
      << std::endl;
    
    return 0;
}
```

Setting flags on the comman dline

```bash
$ cmake .. && make -j && ./uspd --opt2=2 --opt4=4

NAME: uspd
VERSION: 1.0.2
OPTION1: 1
OPTION2: 2
OPTION3: 1
OPTION4: 4

```

## TODO:

 - [ ] Unit tests
 - [ ] Print help
 - [ ] Use more special flags