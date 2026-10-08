const MAX_TEAM_SIZE = 6;
const POKEMON_COUNT = 1025;
const MOVE_COUNT = 934;
const ITEM_COUNT = 571;
const ABILITY_COUNT = 125;

const TYPE_CHART = {
  Normal: { Rock: 0.5, Ghost: 0, Steel: 0.5 },
  Fire: { Fire: 0.5, Water: 0.5, Grass: 2, Ice: 2, Bug: 2, Rock: 0.5, Dragon: 0.5, Steel: 2 },
  Water: { Fire: 2, Water: 0.5, Grass: 0.5, Ground: 2, Rock: 2, Dragon: 0.5 },
  Electric: { Water: 2, Electric: 0.5, Grass: 0.5, Ground: 0, Flying: 2, Dragon: 0.5 },
  Grass: { Fire: 0.5, Water: 2, Grass: 0.5, Poison: 0.5, Ground: 2, Flying: 0.5, Bug: 0.5, Rock: 2, Dragon: 0.5, Steel: 0.5 },
  Ice: { Fire: 0.5, Water: 0.5, Grass: 2, Ice: 0.5, Ground: 2, Flying: 2, Dragon: 2, Steel: 0.5 },
  Fighting: { Normal: 2, Ice: 2, Poison: 0.5, Flying: 0.5, Psychic: 0.5, Bug: 0.5, Rock: 2, Ghost: 0, Dark: 2, Steel: 2, Fairy: 0.5 },
  Poison: { Grass: 2, Poison: 0.5, Ground: 0.5, Rock: 0.5, Ghost: 0.5, Steel: 0, Fairy: 2 },
  Ground: { Fire: 2, Electric: 2, Grass: 0.5, Poison: 2, Flying: 0, Bug: 0.5, Rock: 2, Steel: 2 },
  Flying: { Electric: 0.5, Grass: 2, Fighting: 2, Bug: 2, Rock: 0.5, Steel: 0.5 },
  Psychic: { Fighting: 2, Poison: 2, Psychic: 0.5, Dark: 0, Steel: 0.5 },
  Bug: { Fire: 0.5, Grass: 2, Fighting: 0.5, Poison: 0.5, Flying: 0.5, Psychic: 2, Ghost: 0.5, Dark: 2, Steel: 0.5, Fairy: 0.5 },
  Rock: { Fire: 2, Ice: 2, Fighting: 0.5, Ground: 0.5, Flying: 2, Bug: 2, Steel: 0.5 },
  Ghost: { Normal: 0, Psychic: 0.5, Ghost: 2, Dark: 0.5 },
  Dragon: { Dragon: 2, Steel: 0.5, Fairy: 0 },
  Dark: { Fighting: 0.5, Psychic: 2, Ghost: 2, Fairy: 0.5 },
  Steel: { Fire: 0.5, Water: 0.5, Electric: 0.5, Ice: 2, Rock: 2, Steel: 0.5, Fairy: 2 },
  Fairy: { Fire: 0.5, Fighting: 2, Poison: 0.5, Dragon: 2, Dark: 2, Steel: 0.5 }
};

const POKEMON_NAMES = [
  'Bulbasaur', 'Ivysaur', 'Venusaur', 'Charmander', 'Charmeleon', 'Charizard', 'Squirtle', 'Wartortle', 'Blastoise', 'Caterpie', 'Metapod', 'Butterfree',
  'Weedle', 'Kakuna', 'Beedrill', 'Pidgey', 'Pidgeotto', 'Pidgeot', 'Rattata', 'Raticate', 'Spearow', 'Fearow', 'Ekans', 'Arbok', 'Pikachu', 'Raichu',
  'Sandshrew', 'Sandslash', 'Nidoran', 'Nidorina', 'Nidoqueen', 'Nidorino', 'Nidoking', 'Clefairy', 'Clefable', 'Vulpix', 'Ninetales', 'Jigglypuff', 'Wigglytuff',
  'Zubat', 'Golbat', 'Oddish', 'Gloom', 'Vileplume', 'Paras', 'Parasect', 'Venonat', 'Venomoth', 'Diglett', 'Dugtrio', 'Meowth', 'Persian', 'Psyduck', 'Golduck',
  'Mankey', 'Primeape', 'Growlithe', 'Arcanine', 'Poliwag', 'Poliwhirl', 'Poliwrath', 'Abra', 'Kadabra', 'Alakazam', 'Machop', 'Machoke', 'Machamp', 'Bellsprout',
  'Weepinbell', 'Victreebel', 'Tentacool', 'Tentacruel', 'Geodude', 'Graveler', 'Golem', 'Ponyta', 'Rapidash', 'Slowpoke', 'Slowbro', 'Magnemite', 'Magneton',
  'Farfetchd', 'Doduo', 'Dodrio', 'Seel', 'Dewgong', 'Grimer', 'Muk', 'Shellder', 'Cloyster', 'Gastly', 'Haunter', 'Gengar', 'Onix', 'Drowzee', 'Hypno', 'Krabby',
  'Kingler', 'Voltorb', 'Electrode', 'Exeggcute', 'Exeggutor', 'Cubone', 'Marowak', 'Hitmonlee', 'Hitmonchan', 'Lickitung', 'Koffing', 'Weezing', 'Rhyhorn',
  'Rhydon', 'Chansey', 'Tangela', 'Kangaskhan', 'Horsea', 'Seadra', 'Goldeen', 'Seaking', 'Staryu', 'Starmie', 'MrMime', 'Scyther', 'Jynx', 'Electabuzz',
  'Magmar', 'Pinsir', 'Tauros', 'Magikarp', 'Gyarados', 'Lapras', 'Ditto', 'Eevee', 'Vaporeon', 'Jolteon', 'Flareon', 'Porygon', 'Omanyte', 'Omastar',
  'Kabuto', 'Kabutops', 'Aerodactyl', 'Snorlax', 'Articuno', 'Zapdos', 'Moltres', 'Dratini', 'Dragonair', 'Dragonite', 'Mewtwo', 'Mew', 'Chikorita', 'Bayleef',
  'Meganium', 'Cyndaquil', 'Quilava', 'Typhlosion', 'Totodile', 'Croconaw', 'Feraligatr', 'Sentret', 'Furret', 'Hoothoot', 'Noctowl', 'Ledyba', 'Ledian',
  'Spinarak', 'Ariados', 'Crobat', 'Chinchou', 'Lanturn', 'Pichu', 'Cleffa', 'Igglybuff', 'Togepi', 'Togetic', 'Natu', 'Xatu', 'Mareep', 'Flaaffy', 'Ampharos',
  'Bellossom', 'Marill', 'Azumarill', 'Sudowoodo', 'Politoed', 'Hoppip', 'Skiploom', 'Jumpluff', 'Aipom', 'Sunkern', 'Sunflora', 'Yanma', 'Woobat', 'Swoobat',
  'Pineco', 'Forretress', 'Dunsparce', 'Gligar', 'Steelix', 'Snubbull', 'Granbull', 'Qwilfish', 'Scizor', 'Shuckle', 'Heracross', 'Sneasel', 'Teddiursa', 'Ursaring',
  'Slugma', 'Magcargo', 'Swinub', 'Piloswine', 'Corsola', 'Remoraid', 'Octillery', 'Delibird', 'Mantine', 'Skarmory', 'Houndour', 'Houndoom', 'Kingdra', 'Phanpy',
  'Donphan', 'Porygon2', 'Stantler', 'Smeargle', 'Tyrogue', 'Hitmontop', 'Smoochum', 'Elekid', 'Magby', 'Miltank', 'Blissey', 'Raikou', 'Entei', 'Suicune',
  'Larvitar', 'Pupitar', 'Tyranitar', 'Lugia', 'HoOh', 'Celebi', 'Treecko', 'Grovyle', 'Sceptile', 'Torchic', 'Combusken', 'Blaziken', 'Mudkip', 'Marshtomp',
  'Swampert', 'Poochyena', 'Mightyena', 'Zigzagoon', 'Linoone', 'Wurmple', 'Silcoon', 'Beautifly', 'Cascoon', 'Dustox', 'Lotad', 'Lombre', 'Ludicolo', 'Seedot',
  'Nuzleaf', 'Shiftry', 'Taillow', 'Swellow', 'Wingull', 'Pelipper', 'Ralts', 'Kirlia', 'Gardevoir', 'Surskit', 'Masquerain', 'Shroomish', 'Breloom', 'Slakoth',
  'Vigoroth', 'Slaking', 'Nincada', 'Ninjask', 'Shedinja', 'Whismur', 'Loudred', 'Exploud', 'Makuhita', 'Hariyama', 'Azurill', 'Nosepass', 'Skitty', 'Delcatty',
  'Sableye', 'Mawile', 'Aron', 'Lairon', 'Aggron', 'Meditite', 'Medicham', 'Electrike', 'Manectric', 'Plusle', 'Minccino', 'Cinccino', 'Roselia', 'Roserade',
  'Glalie', 'Spheal', 'Sealeo', 'Walrein', 'Clamperl', 'Huntail', 'Gorebyss', 'Absol', 'Snorunt', 'Froslass', 'Rotom', 'Uxie', 'Mesprit', 'Azelf', 'Dialga',
  'Palkia', 'Heatran', 'Regigigas', 'Giratina', 'Cresselia', 'Phione', 'Manaphy', 'Darkrai', 'Shaymin', 'Arceus'
];

const MOVE_NAMES = [
  'Tackle', 'Thunderbolt', 'Flamethrower', 'Surf', 'Vine Whip', 'Ice Beam', 'Earthquake', 'Psychic', 'Shadow Ball', 'Aerial Ace', 'Focus Blast',
  'Solar Beam', 'Dragon Claw', 'Dark Pulse', 'Stone Edge', 'Flash Cannon', 'Moonblast', 'Waterfall', 'Leaf Storm', 'Thunder Punch', 'Fire Blast',
  'Hydro Pump', 'Giga Drain', 'Blizzard', 'Hyper Beam', 'Close Combat', 'Iron Tail', 'Air Slash', 'Sucker Punch', 'Sludge Bomb', 'Cross Chop',
  'Power Gem', 'Play Rough', 'Ice Punch', 'Wild Charge', 'Brave Bird', 'Aura Sphere', 'Scald', 'Dazzling Gleam', 'Earth Power', 'Ancient Power',
  'Poison Jab', 'Seed Bomb', 'Crunch', 'Foul Play', 'Heat Wave', 'Mist Ball', 'Shadow Sneak', 'XScissor', 'Roost', 'Protect', 'Rapid Spin', 'Endeavor',
  'Recover', 'Leech Seed', 'WillO Wisp', 'Thunder Wave', 'Sleep Powder', 'Explosion', 'Outrage', 'Last Resort', 'Drain Punch', 'Belly Drum', 'Return',
  'Double Edge', 'Facade', 'Knock Off', 'Rock Slide', 'Superpower', 'Zen Headbutt', 'Flash', 'Vine Whip', 'Bubble Beam', 'Shell Smash', 'Night Slash',
  'Assurance', 'Muddy Water', 'Acrobatics', 'Rock Tomb', 'Iron Defense', 'Heavy Slam', 'Gyro Ball', 'Zap Cannon', 'Sweet Scent', 'Sky Attack', 'Crabhammer',
  'Seismic Toss', 'Magnet Bomb', 'Tri Attack', 'Double Hit', 'Meteor Mash', 'Shadow Punch', 'Swords Dance', 'Defog', 'Taunt', 'Substitute', 'Snore', 'Recycle',
  'Future Sight', 'Trick', 'Spikes', 'Stealth Rock', 'Toxic', 'Poison Tail', 'Dragon Rush', 'Brutal Swing', 'Hex', 'Discharge', 'Overheat', 'Iron Head'
];

const ITEM_NAMES = [
  'Expert Belt', 'Life Orb', 'Choice Scarf', 'Choice Specs', 'Leftovers', 'Assault Vest', 'Sitrus Berry', 'Weakness Policy', 'Black Sludge', 'Muscle Band',
  'Wise Glasses', 'Heavy Duty Boots', 'Assault Vest', 'Eject Button', 'King\'s Rock', 'Toxic Orb', 'Flame Orb', 'Quick Claw', 'Focus Sash', 'Mental Herb',
  'Lum Berry', 'Air Balloon', 'Big Root', 'White Herb', 'Power Herb', 'Dragon Fang', 'Poison Barb', 'Sharp Beak', 'Gold Berry', 'Silver Powder', 'Smooth Rock',
  'Mystic Water', 'Zap Plate', 'Earth Plate', 'Soft Sand', 'Hard Stone', 'Adrenaline Orb', 'Red Card', 'Road Light', 'Mega Stone', 'Everstone', 'Berry Juice',
  'Battle Item', 'Fist Plate', 'Mago Berry', 'Iapapa Berry', 'Shed Shell', 'Belue Berry', 'Apt Berry', 'Pomeg Berry', 'Persim Berry', 'Tamato Berry', 'Rindo Berry'
];

const ABILITY_NAMES = [
  'Static', 'Overgrow', 'Torrent', 'Blaze', 'Levitate', 'Pressure', 'Intimidate', 'Swift Swim', 'Flash Fire', 'Volt Absorb', 'Shed Skin', 'Battle Armor',
  'Technician', 'Adaptability', 'Speed Boost', 'Moxie', 'Drought', 'Drizzle', 'Sand Veil', 'Wonder Guard', 'Compound Eyes', 'Shadow Tag', 'Defiant', 'Toxic Boost',
  'Mold Breaker', 'Vital Spirit', 'Rough Skin', 'Cute Charm', 'Storm Drain', 'Motor Drive', 'Guts', 'Magnet Pull', 'Flare Boost', 'Sniper', 'Shell Armor',
  'Contrary', 'Limber', 'Multiscale', 'Filter', 'Insomnia', 'Color Change', 'Solid Rock', 'Iron Fist', 'Run Away', 'Steadfast', 'Prankster', 'Arena Trap',
  'No Guard', 'Big Pecks', 'Unnerve', 'Cursed Body', 'Reckless', 'Huge Power', 'Leaf Guard', 'Inner Focus', 'Skill Link', 'Healer', 'Dry Skin', 'Poison Point'
];

const STAT_KEYS = ['hp', 'attack', 'defense', 'specialAttack', 'specialDefense', 'speed'];

function generatePokemonCatalog() {
  const list = [];
  for (let i = 0; i < POKEMON_COUNT; i += 1) {
    const baseName = POKEMON_NAMES[i % POKEMON_NAMES.length] || `Pokémon ${i + 1}`;
    const suffix = i >= POKEMON_NAMES.length ? ` ${Math.floor(i / POKEMON_NAMES.length) + 1}` : '';
    const types = [
      ['Normal', 'Fire', 'Water', 'Electric', 'Grass', 'Ice', 'Fighting', 'Poison', 'Ground', 'Flying', 'Psychic', 'Bug', 'Rock', 'Ghost', 'Dragon', 'Dark', 'Steel', 'Fairy'][i % 18],
      ['Fairy', 'Normal', 'Fire', 'Water', 'Grass', 'Ice', 'Fighting', 'Poison', 'Ground', 'Flying', 'Psychic', 'Bug', 'Rock', 'Ghost', 'Dragon', 'Dark', 'Steel', 'Fairy'][(i * 3 + 5) % 18]
    ];

    const stats = {};
    for (const key of STAT_KEYS) {
      stats[key] = 40 + ((i * 17 + key.length * 13) % 150);
    }

    list.push({
      id: i + 1,
      name: `${baseName}${suffix}`,
      types,
      sprite: ['⚡', '🌿', '🔥', '💧', '🧊', '🌋', '✨', '🦊', '🐉', '🌙'][i % 10],
      stats,
      abilityId: (i * 7 + 3) % ABILITY_COUNT + 1,
      moveIds: [
        (i * 11 + 3) % MOVE_COUNT + 1,
        (i * 17 + 5) % MOVE_COUNT + 1,
        (i * 23 + 7) % MOVE_COUNT + 1,
        (i * 29 + 9) % MOVE_COUNT + 1
      ]
    });
  }
  return list;
}

function generateMoveCatalog() {
  const list = [];
  for (let i = 0; i < MOVE_COUNT; i += 1) {
    list.push({
      id: i + 1,
      name: MOVE_NAMES[i % MOVE_NAMES.length] || `Move ${i + 1}`,
      type: ['Normal', 'Fire', 'Water', 'Electric', 'Grass', 'Ice', 'Fighting', 'Poison', 'Ground', 'Flying', 'Psychic', 'Bug', 'Rock', 'Ghost', 'Dragon', 'Dark', 'Steel', 'Fairy'][i % 18],
      power: 30 + (i % 80),
      accuracy: 80 + (i % 21),
      category: ['physical', 'special', 'status'][i % 3],
      priority: i % 4 === 0 ? 1 : 0,
      pp: 10 + (i % 18)
    });
  }
  return list;
}

function generateItemCatalog() {
  const list = [];
  for (let i = 0; i < ITEM_COUNT; i += 1) {
    list.push({
      id: i + 1,
      name: ITEM_NAMES[i % ITEM_NAMES.length] || `Item ${i + 1}`,
      effect: ['Attack', 'Defense', 'Speed', 'HP', 'Focus', 'Utility'][i % 6],
      bonus: 6 + (i % 12)
    });
  }
  return list;
}

function generateAbilityCatalog() {
  const list = [];
  for (let i = 0; i < ABILITY_COUNT; i += 1) {
    list.push({
      id: i + 1,
      name: ABILITY_NAMES[i % ABILITY_NAMES.length] || `Ability ${i + 1}`,
      boost: 4 + (i % 15)
    });
  }
  return list;
}

const pokemonCatalog = generatePokemonCatalog();
const moveCatalog = generateMoveCatalog();
const itemCatalog = generateItemCatalog();
const abilityCatalog = generateAbilityCatalog();

const state = {
  playerTeam: [],
  botTeam: [],
  battleRunning: false,
  logEntries: []
};

function getPokemonById(id) {
  return pokemonCatalog.find((pokemon) => pokemon.id === Number(id)) || pokemonCatalog[0];
}

function getMoveById(id) {
  return moveCatalog.find((move) => move.id === Number(id)) || moveCatalog[0];
}

function getItemById(id) {
  return itemCatalog.find((item) => item.id === Number(id)) || itemCatalog[0];
}

function getAbilityById(id) {
  return abilityCatalog.find((ability) => ability.id === Number(id)) || abilityCatalog[0];
}

function getRandomTeam(typeKey) {
  const team = [];
  const seen = new Set();

  while (team.length < MAX_TEAM_SIZE) {
    const randomId = Math.floor(Math.random() * pokemonCatalog.length) + 1;
    if (seen.has(randomId)) continue;
    seen.add(randomId);

    const pokemon = getPokemonById(randomId);
    const moveIds = [
      getMoveIdForPokemon(pokemon, 1),
      getMoveIdForPokemon(pokemon, 2),
      getMoveIdForPokemon(pokemon, 3),
      getMoveIdForPokemon(pokemon, 4)
    ];

    team.push({
      pokemonId: pokemon.id,
      itemId: itemCatalog[(randomId * 7 + (typeKey === 'bot' ? 3 : 1)) % itemCatalog.length].id,
      abilityId: abilityCatalog[(randomId * 13 + (typeKey === 'bot' ? 5 : 2)) % abilityCatalog.length].id,
      moveIds,
      hp: pokemon.stats.hp
    });
  }

  return team;
}

function getMoveIdForPokemon(pokemon, index) {
  const offset = (pokemon.id * (index + 2) * 17) % moveCatalog.length;
  return moveCatalog[offset].id;
}

function renderTeamBoard(teamKey) {
  const board = document.getElementById(`${teamKey}-team`);
  const team = state[teamKey];

  board.innerHTML = team.map((entry, index) => {
    const pokemon = getPokemonById(entry.pokemonId);

    return `
      <div class="team-card">
        <div class="card-head">
          <span class="card-badge">${index + 1}</span>
          <span class="card-name">${pokemon.name}</span>
        </div>

        <div>
          <label class="label">Pokémon</label>
          <select data-team="${teamKey}" data-slot="${index}" data-field="pokemon">
            ${pokemonCatalog.map((option) => `<option value="${option.id}" ${Number(option.id) === Number(entry.pokemonId) ? 'selected' : ''}>${option.name}</option>`).join('')}
          </select>
        </div>

        <div class="config-row">
          <div>
            <label class="label">Move 1</label>
            <select data-team="${teamKey}" data-slot="${index}" data-move-index="0">
              ${renderMoveSelectOptions(entry.moveIds[0])}
            </select>
          </div>
          <div>
            <label class="label">Move 2</label>
            <select data-team="${teamKey}" data-slot="${index}" data-move-index="1">
              ${renderMoveSelectOptions(entry.moveIds[1])}
            </select>
          </div>
          <div>
            <label class="label">Move 3</label>
            <select data-team="${teamKey}" data-slot="${index}" data-move-index="2">
              ${renderMoveSelectOptions(entry.moveIds[2])}
            </select>
          </div>
          <div>
            <label class="label">Move 4</label>
            <select data-team="${teamKey}" data-slot="${index}" data-move-index="3">
              ${renderMoveSelectOptions(entry.moveIds[3])}
            </select>
          </div>
        </div>

        <div class="config-row">
          <div>
            <label class="label">Item</label>
            <select data-team="${teamKey}" data-slot="${index}" data-field="item">
              ${renderItemSelectOptions(entry.itemId)}
            </select>
          </div>
          <div>
            <label class="label">Ability</label>
            <select data-team="${teamKey}" data-slot="${index}" data-field="ability">
              ${renderAbilitySelectOptions(entry.abilityId)}
            </select>
          </div>
        </div>
      </div>
    `;
  }).join('');
}

function renderMoveSelectOptions(selectedId) {
  return moveCatalog.map((move) => `<option value="${move.id}" ${Number(move.id) === Number(selectedId) ? 'selected' : ''}>${move.name}</option>`).join('');
}

function renderItemSelectOptions(selectedId) {
  return itemCatalog.map((item) => `<option value="${item.id}" ${Number(item.id) === Number(selectedId) ? 'selected' : ''}>${item.name}</option>`).join('');
}

function renderAbilitySelectOptions(selectedId) {
  return abilityCatalog.map((ability) => `<option value="${ability.id}" ${Number(ability.id) === Number(selectedId) ? 'selected' : ''}>${ability.name}</option>`).join('');
}

function syncTeamEntry(teamKey, slotIndex, field, value) {
  const team = state[teamKey];
  if (!team[slotIndex]) return;

  if (field === 'pokemon') {
    const newPokemon = getPokemonById(value);
    team[slotIndex].pokemonId = Number(value);
    team[slotIndex].moveIds = [
      getMoveIdForPokemon(newPokemon, 1),
      getMoveIdForPokemon(newPokemon, 2),
      getMoveIdForPokemon(newPokemon, 3),
      getMoveIdForPokemon(newPokemon, 4)
    ];
    team[slotIndex].abilityId = abilityCatalog[(newPokemon.id * 13 + 5) % abilityCatalog.length].id;
    team[slotIndex].itemId = itemCatalog[(newPokemon.id * 7 + 3) % itemCatalog.length].id;
  }

  if (field === 'item') {
    team[slotIndex].itemId = Number(value);
  }

  if (field === 'ability') {
    team[slotIndex].abilityId = Number(value);
  }

  if (field === 'move') {
    team[slotIndex].moveIds[Number(value.index)] = Number(value.moveId);
  }

  renderTeamBoard('player');
  renderTeamBoard('bot');
}

function renderBattleStatus(text, tone='') {
  const status = document.getElementById('battle-status');
  status.textContent = text;
  status.dataset.tone = tone;
}

function updateBattleScene(playerActive, botActive) {
  const playerName = document.getElementById('player-active-name');
  const botName = document.getElementById('bot-active-name');
  const playerSprite = document.getElementById('player-sprite');
  const botSprite = document.getElementById('bot-sprite');

  const playerHpText = document.getElementById('player-hp-text');
  const botHpText = document.getElementById('bot-hp-text');
  const playerHpBar = document.getElementById('player-hp-bar');
  const botHpBar = document.getElementById('bot-hp-bar');

  if (!playerActive || !botActive) {
    playerName.textContent = '-';
    botName.textContent = '-';
    playerSprite.textContent = '⚡';
    botSprite.textContent = '🌿';
    playerHpText.textContent = '0 / 0';
    botHpText.textContent = '0 / 0';
    playerHpBar.style.width = '0%';
    botHpBar.style.width = '0%';
    return;
  }

  playerName.textContent = playerActive.name;
  botName.textContent = botActive.name;
  playerSprite.textContent = playerActive.sprite;
  botSprite.textContent = botActive.sprite;

  const playerHpPct = (playerActive.hp / playerActive.maxHp) * 100;
  const botHpPct = (botActive.hp / botActive.maxHp) * 100;

  playerHpText.textContent = `${playerActive.hp} / ${playerActive.maxHp}`;
  botHpText.textContent = `${botActive.hp} / ${botActive.maxHp}`;
  playerHpBar.style.width = `${Math.max(0, playerHpPct)}%`;
  botHpBar.style.width = `${Math.max(0, botHpPct)}%`;
}

function renderMoveBar(activePokemon) {
  const moveBar = document.getElementById('move-bar');
  if (!activePokemon) {
    moveBar.innerHTML = '';
    return;
  }

  moveBar.innerHTML = activePokemon.moves.map((move) => `
    <button class="move-chip" data-move-name="${move.name}">
      <strong>${move.name}</strong>
      <span>${move.type} • ${move.power} power</span>
    </button>
  `).join('');
}

function appendLog(message) {
  const log = document.getElementById('battle-log');
  const entry = document.createElement('div');
  entry.className = 'log-entry';
  entry.innerHTML = message;
  log.prepend(entry);
}

function getAliveMembers(team) {
  return team.filter((member) => !member.fainted);
}

function getFrontliner(team) {
  const alive = getAliveMembers(team);
  if (!alive.length) return null;
  alive.sort((a, b) => b.speed - a.speed);
  return alive[0];
}

function getBattleMember(entry) {
  const pokemon = getPokemonById(entry.pokemonId);
  const item = getItemById(entry.itemId);
  const ability = getAbilityById(entry.abilityId);
  const currentStats = pokemon.stats;

  return {
    ...entry,
    name: pokemon.name,
    sprite: pokemon.sprite,
    types: pokemon.types,
    maxHp: currentStats.hp + item.bonus + ability.boost,
    hp: currentStats.hp + item.bonus + ability.boost,
    attack: currentStats.attack + item.bonus + ability.boost,
    defense: currentStats.defense + Math.floor(item.bonus / 2),
    specialAttack: currentStats.specialAttack + item.bonus + ability.boost,
    specialDefense: currentStats.specialDefense + Math.floor(item.bonus / 2),
    speed: currentStats.speed + Math.floor(ability.boost / 2),
    item,
    ability,
    moves: entry.moveIds.map((moveId) => getMoveById(moveId)),
    fainted: false
  };
}

function calculateTypeMultiplier(moveType, targetTypes) {
  let multiplier = 1;
  for (const targetType of targetTypes) {
    const chart = TYPE_CHART[moveType] || {};
    multiplier *= chart[targetType] || 1;
  }
  return multiplier;
}

function chooseBestMove(attacker, defender) {
  let bestMove = attacker.moves[0];
  let highestScore = -Infinity;

  for (const move of attacker.moves) {
    const typeBonus = calculateTypeMultiplier(move.type, defender.types);
    const statBias = move.category === 'special' ? attacker.specialAttack : attacker.attack;
    const score = (move.power * typeBonus) + (move.priority * 20) + (statBias * 0.18);
    if (score > highestScore) {
      highestScore = score;
      bestMove = move;
    }
  }

  return bestMove;
}

function resolveAttack(attacker, defender, move, sourceLabel) {
  const typeMultiplier = calculateTypeMultiplier(move.type, defender.types);
  const crit = Math.random() < 0.12;
  const randomFactor = 0.85 + Math.random() * 0.3;
  const attackStat = move.category === 'special' ? attacker.specialAttack : attacker.attack;
  const defenseStat = move.category === 'special' ? defender.specialDefense : defender.defense;
  const baseDamage = ((2 * 100 / 5 + 2) * move.power * (attackStat / Math.max(1, defenseStat)) / 50 + 2);
  const rawDamage = baseDamage * typeMultiplier * randomFactor * (crit ? 1.6 : 1);
  const damage = Math.max(6, Math.round(rawDamage));

  defender.hp = Math.max(0, defender.hp - damage);
  defender.fainted = defender.hp <= 0;

  appendLog(`${sourceLabel} ${attacker.name} used <strong>${move.name}</strong> for ${damage} damage${crit ? ' (critical!)' : ''}.`);

  if (crit) appendLog(`${attacker.name} landed a critical hit!`);
  if (typeMultiplier > 1) appendLog(`It was super effective!`);
  if (typeMultiplier < 1 && typeMultiplier > 0) appendLog(`It was not very effective...`);
  if (typeMultiplier === 0) appendLog(`It had no effect!`);

  if (defender.hp <= 0) {
    appendLog(`${defender.name} fainted!`);
  }
}

async function runBattle() {
  if (state.battleRunning) return;

  state.battleRunning = true;
  document.getElementById('battle-log').innerHTML = '';
  renderBattleStatus('Battle started! The arena is live.', 'battle');

  const playerTeam = state.playerTeam.map(getBattleMember);
  const botTeam = state.botTeam.map(getBattleMember);

  let round = 1;

  while (true) {
    const playerActive = getFrontliner(playerTeam);
    const botActive = getFrontliner(botTeam);

    if (!playerActive || !botActive) break;

    const playerMove = chooseBestMove(playerActive, botActive);
    const botMove = chooseBestMove(botActive, playerActive);

    const order = [
      { side: 'player', actor: playerActive, move: playerMove, target: botActive },
      { side: 'bot', actor: botActive, move: botMove, target: playerActive }
    ].sort((a, b) => b.actor.speed - a.actor.speed);

    for (const action of order) {
      if (action.actor.fainted || action.target.fainted) continue;
      resolveAttack(action.actor, action.target, action.move, action.side === 'player' ? 'Player' : 'Bot');
      updateBattleScene(playerActive, botActive);
      renderBattleStatus(`Round ${round}: ${playerActive.name} vs ${botActive.name}`, 'battle');
      await new Promise((resolve) => setTimeout(resolve, 700));

      if (action.target.fainted) {
        const replacement = getFrontliner(action.side === 'player' ? playerTeam : botTeam);
        if (replacement && replacement !== action.target) {
          if (action.side === 'player') {
            appendLog(`Player sends out <strong>${replacement.name}</strong>!`);
          } else {
            appendLog(`Bot sends out <strong>${replacement.name}</strong>!`);
          }
          updateBattleScene(getFrontliner(playerTeam), getFrontliner(botTeam));
        }
      }
    }

    round += 1;
    if (getAliveMembers(playerTeam).length === 0 || getAliveMembers(botTeam).length === 0) break;
  }

  const remainingPlayer = getAliveMembers(playerTeam).length;
  const remainingBot = getAliveMembers(botTeam).length;

  if (remainingPlayer > remainingBot) {
    renderBattleStatus('Victory! You outlasted the bot team.', 'win');
    appendLog(`<strong>Final result:</strong> Player wins with ${remainingPlayer} Pokémon remaining.`);
  } else if (remainingBot > remainingPlayer) {
    renderBattleStatus('Defeat. The bot team took the win.', 'loss');
    appendLog(`<strong>Final result:</strong> Bot wins with ${remainingBot} Pokémon remaining.`);
  } else {
    renderBattleStatus('Draw! Both sides held their ground.', 'draw');
    appendLog('<strong>Final result:</strong> Draw game.');
  }

  state.battleRunning = false;
  updateBattleScene(getFrontliner(playerTeam), getFrontliner(botTeam));
}

function randomizePlayer() {
  state.playerTeam = getRandomTeam('player');
  renderTeamBoard('player');
  renderBattleStatus('Player roster refreshed.', 'battle');
}

function randomizeBot() {
  state.botTeam = getRandomTeam('bot');
  renderTeamBoard('bot');
  renderBattleStatus('Bot roster refreshed.', 'battle');
}

function savePreset(teamKey) {
  const key = `pokebattle:${teamKey}:preset`;
  localStorage.setItem(key, JSON.stringify(state[teamKey]));
  renderBattleStatus(`${teamKey === 'player' ? 'Player' : 'Bot'} preset saved.`, 'battle');
}

function loadPreset(teamKey) {
  const key = `pokebattle:${teamKey}:preset`;
  const raw = localStorage.getItem(key);
  if (!raw) {
    renderBattleStatus('No saved preset found.', 'battle');
    return;
  }
  state[teamKey] = JSON.parse(raw);
  renderTeamBoard(teamKey);
  renderBattleStatus(`${teamKey === 'player' ? 'Player' : 'Bot'} preset loaded.`, 'battle');
}

function initState() {
  state.playerTeam = getRandomTeam('player');
  state.botTeam = getRandomTeam('bot');
  renderTeamBoard('player');
  renderTeamBoard('bot');
  updateBattleScene(null, null);
}

document.addEventListener('change', (event) => {
  const target = event.target;
  if (!target.matches('select')) return;

  const teamKey = target.dataset.team;
  const slotIndex = Number(target.dataset.slot);

  if (target.dataset.field === 'pokemon') {
    syncTeamEntry(teamKey, slotIndex, 'pokemon', Number(target.value));
    return;
  }

  if (target.dataset.field === 'item') {
    syncTeamEntry(teamKey, slotIndex, 'item', Number(target.value));
    return;
  }

  if (target.dataset.field === 'ability') {
    syncTeamEntry(teamKey, slotIndex, 'ability', Number(target.value));
    return;
  }

  if (target.dataset.moveIndex !== undefined) {
    syncTeamEntry(teamKey, slotIndex, 'move', {
      index: Number(target.dataset.moveIndex),
      moveId: Number(target.value)
    });
  }
});

document.getElementById('randomize-player').addEventListener('click', randomizePlayer);
document.getElementById('randomize-bot').addEventListener('click', randomizeBot);
document.getElementById('battle-btn').addEventListener('click', runBattle);
document.getElementById('save-player').addEventListener('click', () => savePreset('player'));
document.getElementById('load-player').addEventListener('click', () => loadPreset('player'));

initState();
renderBattleStatus('Pick your six and challenge the bot team.', 'battle');
appendLog('<strong>System:</strong> The Pokédex builder is ready. Build your squad and battle!');
appendLog('<strong>Tip:</strong> Save your favorite six before starting a match.');
