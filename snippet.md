```
-- ####################################################################### 
-- ###### List of Highest-scored users (by reputation) from Georgia ######
-- ####################################################################### 
-- * Even though exclusions are applied, some users are still from other countries.
-- * Reputation can be considered a good indicator if that comes from answers (not from questions).

SELECT
    ROW_NUMBER() OVER(ORDER BY Reputation DESC) AS [#], 
    Id AS [User Link], 
    Reputation
    
FROM
    Users
    
WHERE
  (
        lower(Location) LIKE ('%georgia%')
    OR  lower(Location) LIKE ('%,GE')
    OR  lower(Location) LIKE ('% GE')
    OR  lower(Location) LIKE ('%tbilisi%')
    OR  lower(Location) LIKE ('%kutaisi%') 
    OR  lower(Location) LIKE ('%batumi%')
    OR  lower(Location) LIKE ('%rustavi%')
    OR  lower(Location) LIKE ('%zugdidi%')
  )

   -- EXCLUDE NON GEORGIAN results
   and not
  (
       lower(Location) LIKE '%united states%'   -- Exclude United States
    or Location LIKE '%USA%'                    -- Exclude USA 
    or Location LIKE '%U.S.%'                   -- Exclude U.S. 
    or Location LIKE '%US'                      -- Exclude US
    or Location LIKE '% GA%'                    -- Exclude GA  (State of US)
    or lower(Location) LIKE '%atlanta%'         -- Exclude atlanta 
    or lower(Location) LIKE '%german%'          -- Exclude Germany 
    or lower(Location) LIKE '%ital%'            -- Exclude state: GE of Italy/ia
    or lower(Location) LIKE '%netherlands%'     -- Exclude Ge.. of Netherlands
    -- other exclusions can also be applied: https://pastebin.com/WqsQvkNJ
  )
    
ORDER BY
    Reputation DESC;
```
