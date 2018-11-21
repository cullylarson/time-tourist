# Time Tourist

> A text-based adventure game played on a hand-held device.

## Ideas

1. First screen needs to be a menu.
    - Choose map? If only one map, no choice?
    - Choose saved game or new game.
    - Can delete saved games.
    - Saved game names are randomly generated? Might need extra memory. Or could use buttons to select letters to name the game.

1. Need some way to indicate progress (so you could compare progress to other players).

1. Maybe use an SD card for data? Would be easy to load new maps.

1. Grid-based map, but only showing text, so would need to remember where you are.

1. Each tile gets a name, make it easier to remember where you are.

1. There are various actions in the game. Each action has button. Also, direction buttons (north, south, east, west). Each action can use the NSEW buttons to indicate the object of the action (e.g. press and action button then a direction button). The move action doesn't need a button, just press a direction button without first selecting an action.

1. If press an action, it should be clear that the action has been selected (e.g. show text on screen of selected action). If press action button again, will unselect that action.

1. Actions
    - Move
    - Open
    - Close?
    - Get/Pick up
    - Drop
    - Use
    - Talk
    - Look

1. The Look action shows you more details about a direction than what is said in the description.

1. You can only hold four items at a time (e.g. NSEW slots).
    - I like the idea that you'll have to leave items behind to complete certain tasks, but that you'll have to go back and get them for later tasks.
    - I like the idea that some items will seem very important, but will never be used. It will tempt you to keep the item with you.

1. Because each action can only have four objects per tile (i.e. NSEW), can only have four directions to move, four items to pick-up, for spaces to leave items, four people to talk to, etc.

1. Using items will somehow need to change the state of a tile (e.g use the flashlight, see a hidden door).

1. Maybe some items use two slots.

1. Items
    - Keys
    - Letters
    - Flashlight
    - Time machine parts
    - Tools (e.g. for fixing the time machine, or opening areas of the map)

1. Ideally, would be able to have a "map definition" that would dictate the specifics of the map and a generic algorithm for using actions to change the map. That way a map is just a file and could easily create new maps and save games without changing the algorithm.

1. Things on a tile:
    - People
    - Doors/directions
    - Items
    - Objects (maybe these are things that items can be used on)

1. Label all items uniquely, so it will be clear if you've already seen this item. For example, a letter might have a title or just "Letter 189". Oh, maybe even "Journal Page 37".

1. Things in letters could potentially be useful information for solving puzzles.

1. Don't make it necessary to "go back" too far to do anything. Instead, generally progress toward some goal.

1. Need some way to make certain tiles elements appear/function conditionally based on the state of other tiles (e.g. can only open door in tile #20 if switch is "open" on tile #31).

1. Each tile element will need some kind of state. Here are some examples of element states:
    - Can move in this direction
    - Open/closed
    - Item has been used on (will need to record which items)
    - Item can be used on (will need to record which items)
    - Visible/invisible

1. When an item is used on an object, only change the state of a tile if that item *can* be used on that object. No need to store a bunch of useless states of items used on objects that don't change anything.

1. Maybe states can be conditional on a list of other states. E.g. object is visible if: tile #20, object #17 used on element #67. Or: Can move in this direction if: tile #19, object #62 is visible.

1. Maybe have the possibility of a "doorway" in each direction? Could help to clarify when the state of that doorway changes (e.g. if a door opens). If no doorway specified, then it's either a passageway or a wall.

1. Maybe show text in response to actions. For example: show action text when item #17 is used on element #78.

1. Will probably need to write a program to help create maps. Can't do it manually.

1. Since an "open" doorways and objects, will need to only allow one openable doorway or object in any direction. Then when "open" in that direction, the program will just pick the open-able element.

## Plot

You walk up in a room. You don't remember anything. As you make your way through the map, you find letters and people to talk to that fill in your story. You were in the process of making a time machine to e.g. save the world. The time machine is the map; it's huge and you're wandering around inside it. Something happened (e.g. accident) and the machine was damaged and you were injured. You realize you need to fix the time machine. Most of your time is spent doing that. You're also learning more about why you're building the time machine. When you fix the time machine and are about to activate it, you find out something that makes you realize you've misunderstood the reason for the time machine. Maybe someone who's helped you along the way turns out to be evil and will use the machine for bad things. That's the end of the map; sort of a "to be continued" situation for a later map.

So maybe the letters you find are journal pages, with dates and page numbers.

## Notes on the Binary Map Definition

1. Have a list of items, objects, people at the beginning of the file and then reference them in the tiles instead of storing the defintition of each in the tile itself.

1. Maybe have a "file table" that has a list of offsets for various sections of the binary (e.g. tile defintions start here, item definitions start here, etc.). Maybe the reference to each item is it's offset in the file, so can find items quickly.

1. Will need to learn more about how SD card reading works to make this efficient.

1. When considering efficiency, remember that the map will changes. If it's too complicated to re-compute offsets, etc. on change then the efficiencies might not be worth it.

1. Mostly needs to be fast for the microcontroller to read/process/display to the user. Probably don't need to think about saving space.

1. Starting a new game, will just copy the map to the "save" and that's the game. Will make changes directly to that version of the map.

1. Maybe also a section in the header indicating which tile the character is on currently.
