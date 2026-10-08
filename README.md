const POKEMON_COUNT = 1025;
const MOVE_COUNT = 934;
const ITEM_COUNT = 571;
const TEAM_SIZE = 6;

const typePool = [
  'Normal', 'Fire', 'Water', 'Electric', 'Grass', 'Ice', 'Fighting', 'Poison',
  'Ground', 'Flying', 'Psychic', 'Bug', 'Rock', 'Ghost', 'Dragon', 'Dark', 'Steel', 'Fairy'
];

const abilityPool = [
  'Static', 'Overgrow', 'Torrent', 'Blaze', 'Levitate', 'Pressure', 'Intimidate', 'Swift Swim',
  'Flash Fire', 'Volt Absorb', 'Shed Skin', 'Battle Armor', 'Truant', 'Technician', 'Big Pecks',
  'Adaptability', 'Speed Boost', 'Moxie', 'Drought', 'Drizzle', 'Sand Veil', 'Wonder Guard', 'Compound Eyes',
  'Shadow Tag', 'Defiant', 'Toxic Boost', 'Mold Breaker', 'Vital Spirit', 'Rough Skin', 'Cute Charm',
  'Storm Drain', 'Electromorphosis', 'No Guard', 'Run Away', 'Steadfast', 'Prankster', 'Arena Trap',
  'Motor Drive', 'Guts', 'Magnet Pull', 'Flare Boost', 'Sniper', 'Shell Armor', 'Contrary', 'Limber',
  'Multiscale', 'Filter', 'Soul-Heart', 'Insomnia', 'Color Change', 'Solid Rock', 'Iron Fist'
];

const moveNames = [
  'Tackle', 'Thunderbolt', 'Flamethrower', 'Surf', 'Vine Whip', 'Ice Beam', 'Earthquake', 'Psychic',
  'Shadow Ball', 'Aerial Ace', 'Close Combat', 'Solar Beam', 'Dragon Claw', 'Dark Pulse', 'Stone Edge',
  'Flash Cannon', 'Moonblast', 'Waterfall', 'Leaf Storm', 'Thunder Punch', 'Fire Blast', 'Hydro Pump',
  'Giga Drain', 'Avalanche', 'Hyper Beam', 'Focus Blast', 'Iron Tail', 'Air Slash', 'Sucker Punch',
  'Sludge Bomb', 'Cross Chop', 'Power Gem', 'Play Rough', 'Ice Punch', 'Wild Charge', 'Stone Edge',
  'Brave Bird', 'Aura Sphere', 'Scald', 'Dazzling Gleam', 'Blizzard', 'Thunder', 'Earth Power', 'Ancient Power',
  'Poison Jab', 'Seed Bomb', 'Crunch', 'Foul Play', 'Heat Wave', 'Mist Ball', 'Shadow Sneak', 'X-Scissor',
  'Roost', 'Protect', 'Rapid Spin', 'Endeavor', 'Recover', 'Leech Seed', 'Will-O-Wisp', 'Thunder Wave', 'Sleep Powder'
];

const itemNames = [
  'Expert Belt', 'Life Orb', 'Choice Specs', 'Choice Scarf', 'Leftovers', 'Assault Vest', 'Sitrus Berry',
  'Eject Button', 'Weakness Policy', 'Black Sludge', 'Heavy-Duty Boots', 'Muscle Band', 'Wise Glasses',
  'Mental Herb', 'Quick Claw', 'Focus Sash', 'King’s Rock', 'Lum Berry', 'Flame Orb', 'Toxic Orb',
  'Bright Powder', 'Silver Powder', 'Power Herb', 'Mago Berry', 'Iapapa Berry', 'Air Balloon', 'Big Root',
  'White Herb', 'Dragon Fang', 'Poison Barb', 'Sharp Beak', 'Soft Sand', 'Hard Stone', 'Metal Coat',
  'Mystic Water', 'Zap Plate', 'Earth Plate', 'Rose Incense', 'Razor Claw', 'Razor Fang', 'Adrenaline Orb',
  'Room Service', 'Dragon Scale', 'Everstone', 'Poke Doll', 'Rind Berry', 'Luminous Moss', 'Gimmighoul Coin'
];

const pokemonNames = [
  'Bulbasaur', 'Ivysaur', 'Venusaur', 'Charmander', 'Charmeleon', 'Charizard', 'Squirtle', 'Wartortle',
  'Blastoise', 'Caterpie', 'Metapod', 'Butterfree', 'Weedle', 'Kakuna', 'Beedrill', 'Pidgey', 'Pidgeotto', 'Pidgeot',
  'Rattata', 'Raticate', 'Spearow', 'Fearow', 'Ekans', 'Arbok', 'Pikachu', 'Raichu', 'Sandshrew', 'Sandslash',
  'Nidoran♀', 'Nidorina', 'Nidoqueen', 'Nidoran♂', 'Nidorino', 'Nidoking', 'Clefairy', 'Clefable', 'Vulpix', 'Ninetales',
  'Jigglypuff', 'Wigglytuff', 'Zubat', 'Golbat', 'Oddish', 'Gloom', 'Vileplume', 'Paras', 'Parasect', 'Venonat',
  'Venomoth', 'Diglett', 'Dugtrio', 'Meowth', 'Persian', 'Psyduck', 'Golduck', 'Mankey', 'Primeape', 'Growlithe',
  'Arcanine', 'Poliwag', 'Poliwhirl', 'Poliwrath', 'Abra', 'Kadabra', 'Alakazam', 'Machop', 'Machoke', 'Machamp',
  'Bellsprout', 'Weepinbell', 'Victreebel', 'Tentacool', 'Tentacruel', 'Geodude', 'Graveler', 'Golem', 'Ponyta',
  'Rapidash', 'Slowpoke', 'Slowbro', 'Magnemite', 'Magneton', 'Farfetch\'d', 'Doduo', 'Dodrio', 'Seel', 'Dewgong',
  'Grimer', 'Muk', 'Shellder', 'Cloyster', 'Gastly', 'Haunter', 'Gengar', 'Onix', 'Drowzee', 'Hypno',
  'Krabby', 'Kingler', 'Voltorb', 'Electrode', 'Exeggcute', 'Exeggutor', 'Cubone', 'Marowak', 'Hitmonlee',
  'Hitmonchan', 'Lickitung', 'Koffing', 'Weezing', 'Rhyhorn', 'Rhydon', 'Chansey', 'Tangela', 'Kangaskhan',
  'Horsea', 'Seadra', 'Goldeen', 'Seaking', 'Staryu', 'Starmie', 'Mr. Mime', 'Scyther', 'Jynx', 'Electabuzz',
  'Magmar', 'Pinsir', 'Tauros', 'Magikarp', 'Gyarados', 'Lapras', 'Ditto', 'Eevee', 'Vaporeon', 'Jolteon',
  'Flareon', 'Porygon', 'Omanyte', 'Omastar', 'Kabuto', 'Kabutops', 'Aerodactyl', 'Snorlax', 'Articuno',
  'Zapdos', 'Moltres', 'Dratini', 'Dragonair', 'Dragonite', 'Mewtwo', 'Mew', 'Chikorita', 'Bayleef', 'Meganium',
  'Cyndaquil', 'Quilava', 'Typhlosion', 'Totodile', 'Croconaw', 'Feraligatr', 'Sentret', 'Furret', 'Hoothoot',
  'Noctowl', 'Ledyba', 'Ledian', 'Spinarak', 'Ariados', 'Crobat', 'Chinchou', 'Lanturn', 'Pichu', 'Cleffa',
  'Igglybuff', 'Togepi', 'Togetic', 'Natu', 'Xatu', 'Mareep', 'Flaaffy', 'Ampharos', 'Bellossom', 'Marill',
  'Azumarill', 'Sudowoodo', 'Politoed', 'Hoppip', 'Skiploom', 'Jumpluff', 'Aipom', 'Sunkern', 'Sunflora',
  'Yanma', 'Woobat', 'Swoobat', 'Pineco', 'Forretress', 'Dunsparce', 'Gligar', 'Steelix', 'Snubbull', 'Granbull',
  'Qwilfish', 'Scizor', 'Shuckle', 'Heracross', 'Sneasel', 'Teddiursa', 'Ursaring', 'Slugma', 'Magcargo',
  'Swinub', 'Piloswine', 'Corsola', 'Remoraid', 'Octillery', 'Delibird', 'Mantine', 'Skarmory', 'Houndour',
  'Houndoom', 'Kingdra', 'Phanpy', 'Donphan', 'Porygon2', 'Stantler', 'Smeargle', 'Tyrogue', 'Hitmontop',
  'Smoochum', 'Elekid', 'Magby', 'Miltank', 'Blissey', 'Raikou', 'Entei', 'Suicune', 'Larvitar', 'Pupitar',
  'Tyranitar', 'Lugia', 'Ho-Oh', 'Celebi', 'Treecko', 'Grovyle', 'Sceptile', 'Torchic', 'Combusken',
  'Blaziken', 'Mudkip', 'Marshtomp', 'Swampert', 'Poochyena', 'Mightyena', 'Zigzagoon', 'Linoone', 'Wurmple',
  'Silcoon', 'Beautifly', 'Cascoon', 'Dustox', 'Lotad', 'Lombre', 'Ludicolo', 'Seedot', 'Nuzleaf', 'Shiftry',
  'Taillow', 'Swellow', 'Wingull', 'Pelipper', 'Ralts', 'Kirlia', 'Gardevoir', 'Surskit', 'Masquerain', 'Shroomish',
  'Breloom', 'Slakoth', 'Vigoroth', 'Slaking', 'Nincada', 'Ninjask', 'Shedinja', 'Whismur', 'Loudred', 'Exploud',
  'Makuhita', 'Hariyama', 'Azurill', 'Nosepass', 'Skitty', 'Delcatty', 'Sableye', 'Mawile', 'Aron', 'Lairon',
  'Aggron', 'Meditite', 'Medicham', 'Electrike', 'Manectric', 'Plusle', 'Minccino', 'Cinccino', 'Roselia',
  'Roserade', 'Glalie', 'Spheal', 'Sealeo', 'Walrein', 'Clamperl', 'Huntail', 'Gorebyss', 'Absol', 'Snorunt',
  'Glalie', 'Froslass', 'Rotom', 'Uxie', 'Mesprit', 'Azelf', 'Dialga', 'Palkia', 'Heatran', 'Regigigas',
  'Giratina', 'Cresselia', 'Phione', 'Manaphy', 'Darkrai', 'Shaymin', 'Arceus', 'Patrat', 'Purrloin', 'Liepard',
  'Pansage', 'Simisage', 'Pansear', 'Simisear', 'Panpour', 'Simipour', 'Munna', 'Musharna', 'Pidove', 'Tranquill',
  'Unfezant', 'Sewaddle', 'Swadloon', 'Leavanny', 'Cottonee', 'Whimsicott', 'Petilil', 'Lilligant', 'Sandile',
  'Krokorok', 'Krookodile', 'Darumaka', 'Darmanitan', 'Maractus', 'Dwebble', 'Crustle', 'Scraggy', 'Scrafty',
  'Sigilyph', 'Yamask', 'Cofagrigus', 'Tirtouga', 'Carracosta', 'Archen', 'Archeops', 'Tranquill', 'Deino',
  'Zweilous', 'Hydreigon', 'Larvesta', 'Volcarona', 'Cobalion', 'Terrakion', 'Virizion', 'Tornadus', 'Thundurus',
  'Reshiram', 'Zekrom', 'Landorus', 'Kyurem', 'Keldeo', 'Meloetta', 'Genesect'
];

function buildPokemonPool() {
  const pool = [];
  for (let i = 0; i < POKEMON_COUNT; i += 1) {
    const id = i + 1;
    const name = pokemonNames[i] || `Pokémon ${id}`;
    pool.push({
      id,
      name,
      typeA: typePool[i % typePool.length],
      typeB: typePool[(i * 3 + 2) % typePool.length],
      sprite: ['🔥', '💧', '🌿', '⚡', '🪨', '✨'][i % 6],
      stats: {
        hp: 70 + ((id * 17) % 130),
        attack: 50 + ((id * 13) % 150),
        defense: 55 + ((id * 11) % 135),
        speed: 45 + ((id * 19) % 140),
      }
    });
  }
  return pool;
}

function buildMovePool() {
  const pool = [];
  for (let i = 0; i < MOVE_COUNT; i += 1) {
    const name = moveNames[i] || `Move ${i + 1}`;
    pool.push({
      id: i + 1,
      name,
      type: typePool[i % typePool.length],
      power: 20 + ((i * 13) % 90),
      accuracy: 85 + ((i * 7) % 15),
      category: ['physical', 'special', 'status'][i % 3]
    });
  }
  return pool;
}

function buildItemPool() {
  const pool = [];
  for (let i = 0; i < ITEM_COUNT; i += 1) {
    const name = itemNames[i] || `Held Item ${i + 1}`;
    pool.push({
      id: i + 1,
      name,
      bonus: 4 + (i % 15),
      label: ['Attack', 'Defense', 'Speed', 'HP'][i % 4]
    });
  }
  return pool;
}

function buildAbilityPool() {
  const pool = [];
  for (let i = 0; i < 120; i += 1) {
    const name = abilityPool[i] || `Ability ${i + 1}`;
    pool.push({
      id: i + 1,
      name,
      modifier: 3 + (i % 18)
    });
  }
  return pool;
}

const pokemonPool = buildPokemonPool();
const movePool = buildMovePool();
const itemPool = buildItemPool();
const abilityPool = buildAbilityPool();

const state = {
  playerTeam: [],
  botTeam: []
};

function getPokemonById(id) {
  return pokemonPool.find((pokemon) => pokemon.id === Number(id)) || null;
}

function getMoveById(id) {
  return movePool.find((move) => move.id === Number(id)) || movePool[0];
}

function getItemById(id) {
  return itemPool.find((item) => item.id === Number(id)) || itemPool[0];
}

function getAbilityById(id) {
  return abilityPool.find((ability) => ability.id === Number(id)) || abilityPool[0];
}

function getRandomTeam(teamKey) {
  const chosen = [];
  const ids = new Set();

  while (chosen.length < TEAM_SIZE) {
    const next = Math.floor(Math.random() * pokemonPool.length) + 1;
    if (ids.has(next)) continue;
    ids.add(next);

    const pokemon = getPokemonById(next);
    const moves = [
      movePool[(next * 3) % movePool.length].id,
      movePool[(next * 5 + 2) % movePool.length].id,
      movePool[(next * 7 + 4) % movePool.length].id,
      movePool[(next * 11 + 6) % movePool.length].id,
    ];

    chosen.push({
      pokemonId: pokemon.id,
      itemId: itemPool[(next * 7 + (teamKey === 'bot' ? 3 : 1)) % itemPool.length].id,
      abilityId: abilityPool[(next * 13 + (teamKey === 'bot' ? 5 : 2)) % abilityPool.length].id,
      moves,
      hp: pokemon.stats.hp
    });
  }

  return chosen;
}

function hydrateInitialTeams() {
  state.playerTeam = getRandomTeam('player');
  state.botTeam = getRandomTeam('bot');
}

function renderPokemonOptions(selectedId = null) {
  return pokemonPool
    .map((pokemon) => {
      const isSelected = Number(selectedId) === pokemon.id ? 'selected' : '';
      return `<option value="${pokemon.id}" ${isSelected}>${pokemon.name}</option>`;
    })
    .join('');
}

function renderMoveOptions(selectedId = null) {
  return movePool
    .map((move) => {
      const isSelected = Number(selectedId) === move.id ? 'selected' : '';
      return `<option value="${move.id}" ${isSelected}>${move.name}</option>`;
    })
    .join('');
}

function renderItemOptions(selectedId = null) {
  return itemPool
    .map((item) => {
      const isSelected = Number(selectedId) === item.id ? 'selected' : '';
      return `<option value="${item.id}" ${isSelected}>${item.name}</option>`;
    })
    .join('');
}

function renderAbilityOptions(selectedId = null) {
  return abilityPool
    .map((ability) => {
      const isSelected = Number(selectedId) === ability.id ? 'selected' : '';
      return `<option value="${ability.id}" ${isSelected}>${ability.name}</option>`;
    })
    .join('');
}

function renderTeam(teamKey) {
  const target = document.getElementById(`${teamKey}-team`);
  const team = state[teamKey];

  target.innerHTML = team
    .map((entry, slotIndex) => {
      const pokemon = getPokemonById(entry.pokemonId);
      const moveOptions = renderMoveOptions(entry.moves[0]);
      const moveOptions2 = renderMoveOptions(entry.moves[1]);
      const moveOptions3 = renderMoveOptions(entry.moves[2]);
      const moveOptions4 = renderMoveOptions(entry.moves[3]);
      const itemOptions = renderItemOptions(entry.itemId);
      const abilityOptions = renderAbilityOptions(entry.abilityId);

      return `
        <div class="slot-card">
          <div class="slot-header">
            <div class="slot-title"><span class="slot-badge">${slotIndex + 1}</span> ${pokemon?.name || 'Choose Pokémon'}</div>
          </div>
          <div class="member-config">
            <div class="full">
              <span>Pokémon</span>
              <select class="pokemon-select" data-team="${teamKey}" data-slot="${slotIndex}" data-field="pokemonId">
                ${renderPokemonOptions(pokemon?.id || null)}
              </select>
            </div>
            <div class="config-row">
              <div class="full">
                <span>Move 1</span>
                <select class="move-select" data-team="${teamKey}" data-slot="${slotIndex}" data-move-index="0">
                  ${moveOptions}
                </select>
              </div>
              <div class="full">
                <span>Move 2</span>
                <select class="move-select" data-team="${teamKey}" data-slot="${slotIndex}" data-move-index="1">
                  ${moveOptions2}
                </select>
              </div>
              <div class="full">
                <span>Move 3</span>
                <select class="move-select" data-team="${teamKey}" data-slot="${slotIndex}" data-move-index="2">
                  ${moveOptions3}
                </select>
              </div>
              <div class="full">
                <span>Move 4</span>
                <select class="move-select" data-team="${teamKey}" data-slot="${slotIndex}" data-move-index="3">
                  ${moveOptions4}
                </select>
              </div>
            </div>
            <div class="config-row">
              <div class="full">
                <span>Held Item</span>
                <select class="item-select" data-team="${teamKey}" data-slot="${slotIndex}">
                  ${itemOptions}
                </select>
              </div>
              <div class="full">
                <span>Ability</span>
                <select class="ability-select" data-team="${teamKey}" data-slot="${slotIndex}">
                  ${abilityOptions}
                </select>
              </div>
            </div>
          </div>
        </div>
      `;
    })
    .join('');
}

function updateTeam(teamKey, slotIndex, field, value) {
  const team = state[teamKey];
  if (!team[slotIndex]) return;

  if (field === 'pokemonId') {
    const pokemon = getPokemonById(value);
    team[slotIndex].pokemonId = Number(value);
    if (pokemon) {
      team[slotIndex].moves = [
        movePool[(pokemon.id * 3) % movePool.length].id,
        movePool[(pokemon.id * 5 + 2) % movePool.length].id,
        movePool[(pokemon.id * 7 + 4) % movePool.length].id,
        movePool[(pokemon.id * 11 + 6) % movePool.length].id,
      ];
      team[slotIndex].itemId = itemPool[(pokemon.id * 7 + 3) % itemPool.length].id;
      team[slotIndex].abilityId = abilityPool[(pokemon.id * 13 + 5) % abilityPool.length].id;
    }
  }

  if (field === 'move') {
    const moveIndex = Number(value.moveIndex);
    team[slotIndex].moves[moveIndex] = Number(value.moveId);
  }

  if (field === 'itemId') {
    team[slotIndex].itemId = Number(value);
  }

  if (field === 'abilityId') {
    team[slotIndex].abilityId = Number(value);
  }

  renderTeam('player');
  renderTeam('bot');
}

function setBattleSummary(message, type = '') {
  const summary = document.getElementById('battle-summary');
  summary.classList.remove('empty', 'win', 'loss');
  if (type) summary.classList.add(type);
  summary.textContent = message;
}

function appendBattleLog(message) {
  const log = document.getElementById('battle-log');
  const entry = document.createElement('div');
  entry.className = 'log-entry';
  entry.innerHTML = message;
  log.prepend(entry);
}

function buildBattleMon(member) {
  const pokemon = getPokemonById(member.pokemonId);
  const item = getItemById(member.itemId);
  const ability = getAbilityById(member.abilityId);
  return {
    id: member.pokemonId,
    name: pokemon.name,
    sprite: pokemon.sprite,
    hp: pokemon.stats.hp,
    maxHp: pokemon.stats.hp,
    attack: pokemon.stats.attack + item.bonus + ability.modifier,
    defense: pokemon.stats.defense + Math.floor(item.bonus / 2),
    speed: pokemon.stats.speed + Math.floor(ability.modifier / 2),
    moves: member.moves.map((moveId) => getMoveById(moveId)),
    fainted: false,
    item,
    ability
  };
}

function getFirstAlive(team) {
  return team.find((member) => !member.fainted) || null;
}

function chooseMove(member) {
  const move = member.moves[Math.floor(Math.random() * member.moves.length)];
  return move || member.moves[0];
}

function applyMove(attacker, defender, move) {
  const variance = 0.8 + Math.random() * 0.4;
  const crit = Math.random() < 0.12;
  const powerFactor = (move.power * variance) / (defender.defense * 0.8 + 8);
  const attackStrength = attacker.attack * 0.9 + Math.random() * 18;
  const damage = Math.max(8, Math.round((powerFactor + attackStrength / 14) * (crit ? 1.6 : 1)));
  defender.hp = Math.max(0, defender.hp - damage);
  if (defender.hp <= 0) defender.fainted = true;
  return { damage, crit, move };
}

function battleTeams() {
  const playerSquad = state.playerTeam.map(buildBattleMon);
  const botSquad = state.botTeam.map(buildBattleMon);

  const summary = document.getElementById('battle-summary');
  document.getElementById('battle-log').innerHTML = '';
  setBattleSummary('Battle is underway...', '');

  appendBattleLog('<strong>Battle started!</strong> A wild bot team descends into the arena.');

  let turn = 1;
  while (turn <= 20) {
    const playerActive = getFirstAlive(playerSquad);
    const botActive = getFirstAlive(botSquad);

    if (!playerActive || !botActive) {
      break;
    }

    const playerMove = chooseMove(playerActive);
    const botMove = chooseMove(botActive);

    const playerHit = applyMove(playerActive, botActive, playerMove);
    appendBattleLog(`Player ${playerActive.name} used <strong>${playerMove.name}</strong> for ${playerHit.damage} damage${playerHit.crit ? ' (critical!)' : ''}.`);

    if (botActive.fainted) {
      appendBattleLog(`Bot ${botActive.name} fainted. ${botActive.name} is out of the fight.`);
      const nextBot = getFirstAlive(botSquad);
      if (!nextBot) break;
    }

    if (!playerActive.fainted && getFirstAlive(playerSquad) && getFirstAlive(botSquad)) {
      const nextBotActive = getFirstAlive(botSquad);
      const botHit = applyMove(botActive, playerActive, botMove);
      appendBattleLog(`Bot ${botActive.name} used <strong>${botMove.name}</strong> for ${botHit.damage} damage${botHit.crit ? ' (critical!)' : ''}.`);

      if (playerActive.fainted) {
        appendBattleLog(`Player ${playerActive.name} fainted. A new fighter steps in.`);
      }
    }

    turn += 1;
  }

  const remainingPlayer = playerSquad.filter((member) => !member.fainted).length;
  const remainingBot = botSquad.filter((member) => !member.fainted).length;

  if (remainingPlayer > remainingBot) {
    setBattleSummary('Victory! Your team outlasted the bot squad.', 'win');
    appendBattleLog(`<strong>Final result:</strong> You win with ${remainingPlayer} fighters remaining.`);
  } else if (remainingBot > remainingPlayer) {
    setBattleSummary('Defeat. The bot team won this battle.', 'loss');
    appendBattleLog(`<strong>Final result:</strong> The bot wins with ${remainingBot} fighters remaining.`);
  } else {
    setBattleSummary('Draw. Both teams stood their ground.', '');
    appendBattleLog('<strong>Final result:</strong> The matchup ended in a draw.');
  }
}

document.addEventListener('change', (event) => {
  const target = event.target;

  if (target.classList.contains('pokemon-select')) {
    const teamKey = target.dataset.team;
    const slotIndex = Number(target.dataset.slot);
    const value = Number(target.value);
    const team = state[teamKey];
    team[slotIndex] = {
      pokemonId: value,
      itemId: itemPool[(value * 7 + 3) % itemPool.length].id,
      abilityId: abilityPool[(value * 13 + 5) % abilityPool.length].id,
      moves: [
        movePool[(value * 3) % movePool.length].id,
        movePool[(value * 5 + 2) % movePool.length].id,
        movePool[(value * 7 + 4) % movePool.length].id,
        movePool[(value * 11 + 6) % movePool.length].id,
      ],
      hp: getPokemonById(value)?.stats.hp || 100
    };
    renderTeam('player');
    renderTeam('bot');
    return;
  }

  if (target.classList.contains('move-select')) {
    const teamKey = target.dataset.team;
    const slotIndex = Number(target.dataset.slot);
    const moveIndex = Number(target.dataset.moveIndex);
    const moveId = Number(target.value);
    state[teamKey][slotIndex].moves[moveIndex] = moveId;
    return;
  }

  if (target.classList.contains('item-select')) {
    const teamKey = target.dataset.team;
    const slotIndex = Number(target.dataset.slot);
    state[teamKey][slotIndex].itemId = Number(target.value);
    return;
  }

  if (target.classList.contains('ability-select')) {
    const teamKey = target.dataset.team;
    const slotIndex = Number(target.dataset.slot);
    state[teamKey][slotIndex].abilityId = Number(target.value);
    return;
  }
});

document.getElementById('randomize-player').addEventListener('click', () => {
  state.playerTeam = getRandomTeam('player');
  renderTeam('player');
  setBattleSummary('Your team has been refreshed with a new six-Pokémon roster.', '');
});

document.getElementById('randomize-bot').addEventListener('click', () => {
  state.botTeam = getRandomTeam('bot');
  renderTeam('bot');
  setBattleSummary('The bot team has been randomly rebuilt.', '');
});

document.getElementById('randomize-bot-team').addEventListener('click', () => {
  state.botTeam = getRandomTeam('bot');
  renderTeam('bot');
  setBattleSummary('The bot team has been rebuilt with a fresh lineup.', '');
});

document.getElementById('battle-btn').addEventListener('click', battleTeams);

hydrateInitialTeams();
renderTeam('player');
renderTeam('bot');
setBattleSummary('Your team is ready. Pick your six and battle the bot.', '');
