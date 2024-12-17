# Project2
// Initialize the player's and computer's health to 100.
let playerHealth = 100;
let computerHealth = 100;

// Display the available moves to the player.
console.log("\nYou and the computer can use these moves:");
console.log("1. Strike: Moderate damage (18-25)");
console.log("2. Power Strike: Big damage, but unpredictable (10-35)");
console.log("3. Heal: Heals yourself (18-25)\n");

// Function to generate a random number between two values (inclusive).
function getRandom(min, max) {
    return Math.floor(Math.random() * (max - min + 1)) + min;
}

// Start a loop that runs until either the player or the computer's health is 0.
while (playerHealth > 0 && computerHealth > 0) {
    // Display current health of both the player and computer.
    console.log(`\nYour health: ${playerHealth}, Computer's health: ${computerHealth}`);
    console.log("Your Turn! Choose your move:");
    console.log("1. Strike");
    console.log("2. Power Strike");
    console.log("3. Heal");

    // Get the player's move.
    let move = parseInt(prompt("Enter 1, 2, or 3: "));

    if (isNaN(move) || move < 1 || move > 3) {
        console.log("Invalid choice! Please enter 1, 2, or 3.");
        continue; // Skip to the next iteration of the loop.
    }

    // Execute the player's move.
    if (move === 1) { // Strike
        let damage = getRandom(18, 25);
        computerHealth -= damage;
        console.log(`You used Strike! You dealt ${damage} damage.`);
    } else if (move === 2) { // Power Strike
        let damage = getRandom(10, 35);
        computerHealth -= damage;
        console.log(`You used Power Strike! You dealt ${damage} damage.`);
    } else if (move === 3) { // Heal
        let heal = getRandom(18, 25);
        playerHealth = Math.min(playerHealth + heal, 100);
        console.log(`You used Heal! You healed ${heal} health.`);
    }

    // Check if the computer's health has dropped to 0 or below.
    if (computerHealth <= 0) {
        console.log("\nThe computer fainted. You win!");
        break;
    }

    // Computer's turn to make a move.
    console.log("\nComputer's Turn!");
    let computerMove;

    if (computerHealth <= 35 && Math.random() < 0.6) { // Heal if health is low.
        computerMove = 3;
    } else {
        computerMove = getRandom(1, 2); // Randomly choose Strike or Power Strike.
    }

    // Execute the computer's move.
    if (computerMove === 1) { // Strike
        let damage = getRandom(18, 25);
        playerHealth -= damage;
        console.log(`The computer used Strike! It dealt ${damage} damage.`);
    } else if (computerMove === 2) { // Power Strike
        let damage = getRandom(10, 35);
        playerHealth -= damage;
        console.log(`The computer used Power Strike! It dealt ${damage} damage.`);
    } else if (computerMove === 3) { // Heal
        let heal = getRandom(18, 25);
        computerHealth = Math.min(computerHealth + heal, 100);
        console.log(`The computer used Heal! It healed ${heal} health.`);
    }

    // Check if the player's health has dropped to 0 or below.
    if (playerHealth <= 0) {
        console.log("\nYou fainted. The computer wins!");
        break;
    }
}
