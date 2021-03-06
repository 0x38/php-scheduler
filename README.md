php-scheduler
============

[![Code Climate](https://codeclimate.com/github/pmill/php-scheduler/badges/gpa.svg)](https://codeclimate.com/github/pmill/php-scheduler) [![Test Coverage](https://scrutinizer-ci.com/g/pmill/php-scheduler/badges/quality-score.png?b=master)](https://scrutinizer-ci.com/g/pmill/php-scheduler/) ![Downloads](https://poser.pugx.org/pmill/php-scheduler/downloads)

Introduction
------------

This package contains a simple PHP cron task scheduler that helps you version control your cron jobs.

Requirements
------------

This library package requires PHP 5.4 or later and a linux operating system.

Installation
------------

### Installing via Composer

The recommended way to install php-scheduler is through
[Composer](http://getcomposer.org).

```bash
# Install Composer
curl -sS https://getcomposer.org/installer | php
```

Next, run the Composer command to install the latest version of php-scheduler:

```bash
composer.phar require pmill/php-scheduler
```

After installing, you need to require Composer's autoloader:

```php
require 'vendor/autoload.php';
```

Once you've created your task list script (see Usage below) open a linux shell add the following line to crontab (crontab -e):

    * * * * * php /path/to/your/task/list/script.php
    

Usage
-----

The following example shows how to schedule a HelloDaily task (simple echo example) and a ShellMonday task (running a shell task example).

    class HelloDailyTask extends \pmill\Scheduler\Task\Task
    {
        public function run()
        {
            $this->setOutput('Hello World');
        }
    }
    
    class ShellMondayTask extends \pmill\Scheduler\Task\Shell
    {
        protected $command = "echo Hello Monday";
    }

    $taskList = new \pmill\Scheduler\TaskList;
    
    // Add task to run at 15:04 every day
    $taskList->addTask((new HelloDailyTask)->setExpression('4 15 * * *'));
    
    // Add task to run at 15:04 every Monday
    $taskList->addTask((new ShellMondayTask)->setExpression('4 15 * * 1'));
    
    $taskList->run();
    $output = $taskList->getOutput();


Version History
---------------

0.1.5 (13/03/2019)

* Resolve list of tasks due before running the tasks (thanks [jhoughtelin](https://github.com/jhoughtelin))

0.1.4 (25/01/2018)

*   Removed nesbot/carbon dependency

0.1.3 (24/05/2015)

*   Added unit tests

0.1.2 (13/05/2015)

*   Fixed missing output bug

0.1.1 (06/02/2015)

*   Fixed incorrect paths

0.1.0 (06/02/2015)

*   First public release of php-scheduler


Copyright
---------

php-scheduler
Copyright (c) 2015 pmill (dev.pmill@gmail.com) 
All rights reserved.
