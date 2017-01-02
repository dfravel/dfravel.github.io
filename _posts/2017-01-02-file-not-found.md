---
title:  "File Not Found"
header:
  overlay_image: "/assets/images/matrix-background.jpg"
  teaser: "/assets/images/trait-not-found.png"
excerpt: "Sometimes the default error message will lead you on a two-hour wild goose chase and have you re-writing your apps and questioning your sanity." 
categories: 
  - Laravel
tags:
  - errors
---

# File Not Found
I spent almost 2 hours updating a registration site for a 2017 event. Step 1 of the update was to do the standard:
```
git pull
composer update
```
and then fix the handful of "package abandoned" error messages and hope that nothing within the 5.2.x upgrade of Laravel caused breaks in my code.

Everything was working great until I needed to call the "SendConfirmation" trait. That's when I saw this:

![not found](/assets/images/trait-not-found.png)

I looked multiple times at the controller code: 

```
<?php
namespace App\Http\Controllers;

use Illuminate\Http\Request;
use App\User;
use App\Registration;
use Auth;
use App\Http\Requests;
use App\Http\Controllers\Controller;
use Illuminate\Database\Eloquent\SoftDeletes;
use App\Http\Requests\SaveContactInformation;
use App\Http\Requests\SaveProfileInformation;
use App\Http\Requests\SavePackageInformation;
use App\Traits\SendConfirmation;
use DB;

class RegistrationController extends Controller
{
	use SendConfirmation;

	public function __construct()
	{
		$this->middleware('auth');
	}
```

It looked perfectly normal. There were no changes at all from the last time we ran this app. Granted, the app hadn't been used since April 2016 and it was a very Laravel versions back, but the controller and trait files hadn't been changed by me or Sue since we archived the app. 

The trait itself was in the Traits folder with the correct namespacing:

```
<?

namespace App\Traits;

use App\User;
use App\Registration;
use App\Registered;
use Auth;
use Mail;
use DB;

trait SendConfirmation {
```

Maybe you've already seen the problem with the code, but it took me over two hours and finally the help of Sue looking over my shoulder as we went through every line of code and log file output. 

During those two hours I moved the trait to a new location; I rewrote portions of it; I changed the function name and took out one line at a time trying to get to the bottom of it. I DD'd every line of code I could and I seriously considered scrapping the trait and rewriting the functions within the Controller. I also started to think deep thoughts about re-writing the entire application (how hard could it be?).

## The Problem and Solution
The problem was in the first line of the trait code. No, not `trait SendConfirmation{`

It was the differennce between `<?` and `<?php'`

My trait file didn't have `<?php'`

## The Moral of the Story
There are a few morals to this story:

1. Sometimes the default error message will send you down the wrong path. 
2. When tracking down bugs, look for the easiest possible solution first
3. Have Sue around to help you troubleshoot. She's pretty smart
4. Apparently, there's a difference between `<?` and `<?php` 
