Rubywarrior-level-6
===================
class Player
   
  def play_turn(warrior)
    variables(warrior)
    moves(warrior)
  end

 def variables(warrior)
   #health warrior, if warrior either is attacked or not
    @perfecthealth = 20
    if @health == nil then @health = @perfecthealth end
    @damagin = warrior.health < @health
  end

  def moves(warrior)
    #The warrior movements
    if warrior.feel(:backward).empty? and @captives != 1
      warrior.walk!(:backward)
    elsif warrior.feel(:backward).empty? == false
      warrior.rescue!(:backward)
      @captives = 1
    else
      if @damagin == true and warrior.feel.empty?
        if warrior.health < 10
          warrior.walk!(:backward)
        else
          warrior.walk!
        end
      elsif @damagin == true and warrior.feel.empty? == false
          warrior.attack!
      elsif @damagin == false and warrior.feel.empty? and warrior.health == @perfecthealth
        warrior.walk!
      elsif @damagin == false and warrior.feel.empty? == false and warrior.health == @perfecthealth
        warrior.attack!
      elsif @damagin == false and warrior.health < @perfecthealth
        warrior.rest!
      end
    end
    @health = warrior.health 
  end
 
end
