+++
date = "2015-08-22"
title = "About"
+++

_Self-taught web developer living in the beautiful Piedmont of NC_

```ruby
class matt_king
  belongs_to:  [:beautiful_daughter, :lovely_wife]
  
  attr_reader :birth_place
  attr_accessor :interests

  def initialize
    @interests = ['hiking', 'cooking', 'reading', 'gaming', 'coding']
    @birth_place = 'Asheville, North Carolina'
  end

  def current_stats
    age = 35
    career = 'web developer'
    place = 'Raleigh, North Carolina'
  end

  def skill_set
    programming_languages = ['Ruby', 'JavaScript']
    frameworks = {'front_end': 'Bulma, Bootstrap', 'back_end': 'Rails'}
  end
end
```