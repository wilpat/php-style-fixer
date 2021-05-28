# PHP Style Fixer

A package aimed at helping a team adopt a uniform set of php coding styles / rules with each other.
## Intallation

Add the repo to your composer.json:
```
"repositories": [
        {
            "type": "github",
            "url": "https://github.com/Thunderbite/php-cs-fixer"
        }
    ]
```

Require the package
`$ composer require wilpat/php-style-fixer`

# Setup
Create a `.php_cs.dist` file inside the root folder of your project and specify the folders you want to be targeted for style fixing as shown below:
```
<?php

$finder = PhpCsFixer\Finder::create()
  ->in([
    __DIR__.'/app',
    __DIR__.'/config',
    __DIR__.'/database',
    __DIR__.'/routes',
    __DIR__.'/tests',
  ]);

return CodeStyleFixer\styles($finder);
```
The above takes in the default folders that come with a laravel app.

# Optional Configuration
You can add your own array of rule sets by editing returning `CodeStyleFixer\styles($finder, $new_rules_array);`
You can also clone this package and edit the rules in `src/rules.php` to have your own coding standard for your team


# Style fixing
## Option 1
Run `./vendor/bin/php-cs-fixer fix` and all the files would get fixed according to the rules you set.

## Option 2 -- Autofix On Save (VSCODE)
If you want automatic fixing on save,
Install this extension called [Run On Save](https://marketplace.visualstudio.com/items?itemName=emeraldwalk.RunOnSave#:~:text=Run%20On%20Save%20for%20Visual,don%27t%20trigger%20the%20commands.) on your vscode
Go to your vscode settings.json file and add these:
```
"emeraldwalk.runonsave": {
    "commands": [
        {
            "match": "\\.php$",
            "cmd": "./vendor/bin/php-cs-fixer fix"
        }
    ]
},
```
Auto fix would kick in upon saving any php file.

## Option 3 -- Fix before push to git
If you want to run the fixer before pushing to git, you can add this script to your package.json file:
`"git": "func() { ./vendor/bin/php-cs-fixer fix && git add . && git commit -m \"$1\" && git push origin HEAD; }; func"`
Now when you want to do a git push, you don't need to do the traditional:
git add .
git commit -m""
git push

Just run npm run git -- "Sample commit message" in your terminal and this would:
Run the fixer
Do your git add, git commit, and push to the current branch you're working on.




