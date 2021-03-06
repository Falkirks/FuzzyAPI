> This tool is primarily a joke and an a silly pleasure project. It is not intended for use on production servers.

Fuzzy
=====
###### Making PocketMine-MP huggable

Fuzzy is multi-purpose life saving tool for PocketMine-MP. It increases huggability by a factor of 10, guaranteed. 

### What is Fuzzy?
Fuzzy is a PocketMine plugin library to make doing stuff easier. Fuzzy wraps around the PocketMine server and enhances plugin development. Fuzzy includes many standard methods and classes along with a powerful intermediary event system.

### How do I setup Fuzzy?
**Warning!** Although cuddly, Fuzzy is extremely invasive. Make sure you understand what you are doing when enabling this plugin.

To activate Fuzzy for your plugin just add the following line to your `plugin.yml`
```yaml
depend: ["FuzzyAPI"]
```
**Note:** If you don't add this, Fuzzy will **not** generate an API object for your plugin, they can't be generated later.

It is recommended that your plugin extend `fuzzy\utils\FuzzyPlugin` instead of `pocketmine\plugin\PluginBase`. Doing so will add a convenience method for accessing the Fuzzy API and add type hinting.

### How do I use Fuzzy?
Fuzzy is available in the `fuzzy` field of your plugin  and can be accessed directly or through `getFuzzy()` (if you plugin extends `FuzzyPlugin`). Your Fuzzy API can be accessed at anytime and doesn't depend on the Fuzzy plugin being enabled.

```php
$this->getFuzzy()->sendFuzz(); // Prints "Fuzzy ❤  PluginName" to console
$this->getFuzzy()->getPlayers(); // Returns a list of online players
```

### What is a fuzzied class? How do they work?
Fuzzy likes to hug things. When a class is fuzzied it means that Fuzzy is encapsulating the original object and providing extra functionality. Fuzzied objects are **not** entirely compatible with the object they are encapsulating, the notable example is

```php
$p = $this->getFuzzy()->getPlayer("Bob"); // Returns "FuzziedPlayer"
var_dump(($p instanceof Player)); // Prints "false"
var_dump(($p->unfuzz() instanceof Player)); // Prints "true" 
```

Fuzzied classes are generated when interacting with the server through the `FuzzyAPI` class. They can also be automatically injected into events passed to your plugin (this is opt-in). If you want to manually fuzz something you can use `$this->getFuzzy()->fuzz($object)`.

### What about this "event system"?
Fuzzy expose a smart event system with a JS like syntax. Fuzzied classes which extend `FuzziedEmitter` can emit events. Here is an example where I listen to all player chat messages
```
$this->getFuzzy()->on("player.chat", function(PlayerChatEvent $event){

});
```
But it gets more powerful, I can listen to the next chat message of a specific player
```
$this->getFuzzy()->getPlayer("bob")->once("chat", function(PlayerChatEvent $event){
    
});
```
### What can I do with Fuzzy?
Not much right now, but features are in the works. Nevertheless, you can still do some cool stuff

```php
$p = $this->getFuzzy()->getPlayer("GrieferTheGriefer");
$p->repeat(5)->until((20/5) * 28)->sendMessage("You are a griefer, nobody likes you, we will kick you soon.");
$p->delay(30 * 20)->kick();
```
### Can I submit Fuzzy plugins to the repository?
You can try. Fuzzy is hacky in nature and doesn't expose efficient ways to do things. 

