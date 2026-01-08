# Requirements

Building a community for managing, promoting, collecting metrics for your player as it saunters through the battlefield.

Where groups of friends collectively rank/score against other same collectives exist.  

Where combat is scored and recorded for winners of campaigns or challenges.

Each playee will be issued its beacon_token, used as a salt with each specialists playing warrior. 

Google, and any other top five openid organizations can be authorizors of playees credentials, etc.

--- Build out api's for the above
---- Landing Single Page app for:
------ Meeting user
--------Do you have an account?
----------No
-------------Redirect to branded - single page app for community/user registration
----------Yes
------------Logged In?
------------No
--------------Redirect to Home page landing page.
------------Yes
--------------Continue
----------------Start beacon here - becon has id?
-------------------No - Create new beacon, register and save

Build campaign for gameplay, with your playee token as owner
-- share
-- registeer
-- play
-- score
-- judge
-- eventover

Requirements:

Server management needs automater.
-- Restart, pick up data for all playees - register to api - respond to events/actions/hooks.
-- Report health
-- HealthReports
-- Ping
-- Etc
-- Start game session
-- make sure sesion healthy and active
-- terminate, restart where failed.

-- technology server side, at the core Apache Iceberg
--- technology choices now - https://iceberg.apache.org/spark-quickstart/#adding-a-catalog

Iceberg will be our interface as orgazniation, with communities, groups, friends - that tracks specialists in the gamescape being watched, monitored, applauded each week.

-- Build for me brief overview, profressionally gamified in graphics.  Simple to use, concise though in technoology supporting and growing friendships. 
-- Spec out data endpoint, relations, and goals for running backend
-- Talk about automation and infrastructure as code is required from the started.

