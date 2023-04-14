<script>
	// Dynamic variables
	let copied = false;
	let surname = "Doe";
	let lettersToCode = ""
	let codedSurname = "";
	
	// Reference constants
	let soundexCoding = {
		"b": 1, "p": 1, "f": 1, "v": 1,
		"c": 2, "s": 2, "k": 2, "g": 2, "j": 2, "q": 2, "x": 2, "z": 2,
		"d": 3, "t": 3,
		"l": 4,
		"m": 5, "n": 5,
		"r": 6
	} // Soundex Coding Chart
	let skippedConsonants = ["W", "H", "Y"];
	let vowels = ["A", "O", "E", "I", "U"]
	
	// Remove invalid consonants for step 2
	function removeInvalidConsonants(surname) {
		// Create an array from the surname
		let surnameChars = surname.toUpperCase();
		// Create the export variable
		var exportedLetters = ""
		
		// Loop over each string in the surname
		for (let surnameChar of surnameChars) {
			var counter = 1
			// Loop over each invalid Consonant
			skippedConsonants.forEach(skippedConsonant => {
				// Check if the current string is a skipped consonant
				if (surnameChar != skippedConsonant && counter == 3) {
					// If the string is not a skipped consonant and you've looped over the 3 invalid consonants, export the current string
					exportedLetters += surnameChar
				} else if (surnameChar != skippedConsonant){
					// If the string is an invalid consonant but you haven't looped over all 3 invalid consonants, increase the counter
					counter += 1
				}
			}) 
		}
		
		console.log(surnameChars, exportedLetters);
		return exportedLetters
	}
	
	// Remove duplicate numbers
	function removeDuplicateLetters(surname) {
		// Create an array from the surname
		let surnameChars = surname.toUpperCase().split("");
		// Create the export variable
		var exportedLetters = ""
		// Create the skip step variable
		var skipNextStep = false
		
		// Loop over each string in the surname
		for(let i = 0; i < surnameChars.length; i++) {
			// Skip if skip step variable is true
			if (skipNextStep) {
				skipNextStep = false
				continue
			} else {
				// Add the current string to the export variable
				exportedLetters += surnameChars[i];
				// Check if i has reached the max value to avoid an out of bounds error 
				if(i != surnameChars.length - 1) {
					// If the current string is the same as the next string, skip the next step
					if(surnameChars[i] == surnameChars[i+1]) {
						skipNextStep = true 
					}
				}
			}
		}
		
		console.log(exportedLetters);
		return exportedLetters
	}
	
	// Check if a letter is a vowel
	function isLetterVowel(char) {
		var isVowel = false
		
		// Check if the current string is a vowel
		vowels.forEach(vowel => {
			if (char == vowel) {
				isVowel = true
			}
		}) 
		
		return isVowel
	}
	
	// Remove letters with the same code
	function removeSameCodeLetters(surname) {
		// Create an array from the surname
		let surnameChars = surname.toLowerCase().split("");
		// Set the maximum value before going out of bounds
		let max = surnameChars.length - 1
		// Variables
		var exportedLetters = ""
		var currLetterCode = 0
		var nextLetterCode = 0
		var skipNextStep = false
		
		// Loop over each string
		for(let i = 0; i < surnameChars.length; i++) {
			// Skip next step if the skip step variable is set to true
			if (skipNextStep) {
				skipNextStep = false
				continue
			} else {
				// Check if the current string is a vowel, if so skip it
				if (isLetterVowel(surnameChars[i].toUpperCase())) {
					continue
				} else if (i != max) {
					// Check if the next string is a vowel
					if (isLetterVowel(surnameChars[i+1].toUpperCase())) {
						// If so, export current string
						exportedLetters += surnameChars[i]
					} else {
						// Calculate the soundex codes of the current and next string
						currLetterCode = soundexCoding[surnameChars[i].toLowerCase()]
						nextLetterCode = soundexCoding[surnameChars[i+1].toLowerCase()]
						
						// Check if the current string has the same code as the next one
						if(currLetterCode == nextLetterCode) {
							// If so, skip the next string
							skipNextStep = true
						}
						// Export the current string
						exportedLetters += surnameChars[i]
					}
				} else {
					exportedLetters += surnameChars[i]
				}
			}
		}
		
		console.log(exportedLetters);
		return exportedLetters
	}
	
	// Code the remaining letters
	function codeLetters(letters) {
		// Create an array based on the remaining letters
		let lettersToCode = letters.toLowerCase()
		// Variables
		var exportedCode = ""
		
		// Loop over each letter
		for (let letter of lettersToCode) {
			// Replace the letter with the corresponding code
			exportedCode += soundexCoding[letter]
		}
		
		// If there's less than three coded letters
		if(exportedCode.length < 3) {
			// Calculate how many missing spots there are for the code
			let missingSpots = 3 - exportedCode.length
			
			// Fill those spots with a 0
			for(let i = 0; i < missingSpots; i++) {
				exportedCode += "0"
			}
		} 
		// Check if there's more than 3 coded letters
		else if (exportedCode.length > 3) {
			// Temporary variables
			let tempArray = exportedCode
			var tempExport = ""
			
			// Export the first three letters of the code
			for(let i = 0; i < 2; i++) {
				tempExport += tempArray[i]
			}
			exportedCode = tempExport
		}
		console.log(lettersToCode, exportedCode);
		return exportedCode
	}
	
	function convertToSoundex(surname) {
		// STEP 1B - Add the first letter to the coded surname
		codedSurname = "";
		copied = false;
		codedSurname += (surname[0]).toUpperCase()
		
		// STEP 1B - If the 1st and 2nd letter are have the same code ignore the second letter
		// Find soundex code for the 1st letter
		let firstLetterCode = soundexCoding[surname.charAt(0).toLowerCase()] 
		// Find soundex code for the 2nd letter
		let secondPosition = 1;
		/*while(isLetterVowel(surname[secondPosition].toUpperCase()) || secondPosition != surname.length-1) {
			console.log(secondPosition, surname.length);
			secondPosition++;	
		}*/
		while(secondPosition != surname.length-1) {
			if(!isLetterVowel(surname[secondPosition].toUpperCase())) {
				break;
			} else {
				secondPosition++;
			}
		}
		if(secondPosition==surname.length-1) {
			secondPosition = 1;
			console.log(secondPosition);
		}
		let secondLetter = surname[secondPosition]
		
		
		 
		let secondLetterCode = soundexCoding[secondLetter.toLowerCase()]
		
		// Check if the code is the same between the first and the second letter
		if (firstLetterCode == secondLetterCode) {
			// If so, ignore the second letter
			console.log(firstLetterCode, secondLetter, "Ignored second letter");
			lettersToCode = surname.slice(secondPosition+1).toLowerCase()
		} else {
			// Otherwise, use all of the remaining letters
			console.log(firstLetterCode, secondLetter, "Kept second letter");
			lettersToCode = surname.slice(secondPosition).toLowerCase()
		} 
		
		// STEP 2 - Remove invalid consonants
		lettersToCode = removeInvalidConsonants(lettersToCode)
		
		// STEP 3 - Remove duplicate adjacent letters 
		lettersToCode = removeDuplicateLetters(lettersToCode)
		
		// STEP 4 & 5 -  Remove letters with the same code that are not separated by a vowel and remove vowels
		lettersToCode = removeSameCodeLetters(lettersToCode)
		
		// STEP 6 & 7 - Code the remaining letters
		codedSurname += codeLetters(lettersToCode)
		console.log(`Surname: ${surname}\nCoded Surname: ${codedSurname}`)
	}
	
	function copyToClipboard(){
		copied = true;
		navigator.clipboard.writeText(codedSurname);
	}
</script>

<div class="mx-auto max-w-7xl px-4 sm:px-6 md:px-8">
	<h1 class="text-2xl font-semibold text-gray-900">Soundex Converter</h1>
</div>
<div class="mx-auto max-w-7xl px-4 sm:px-6 md:px-8 py-4">
	<div id="results" class="mt-4 p-4 border border-gray-300 rounded-md shadow-sm">
		<div class="flex flex-col md:flex-row sm:gap-3">
			<!-- Name -->
			<div class="flex items-center w-[100%] mb-3 sm:w-[50%] sm:mb-0">
				<label for="name" class="inline-block text-sm font-medium text-gray-700" >Surname</label>
				<div class="ml-4">
					<input type="text" bind:value={surname} name="name" id="name" class="block rounded-md border-gray-300 shadow-sm focus:border-blue-500 focus:ring-blue-500 sm:text-sm" placeholder="Doe" aria-describedby="name-description">
				</div>
			</div>
			<button class="rounded-md bg-white px-2.5 py-1.5 h-12 sm:h-[38px] sm:w-[50%] text-sm font-semibold text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 hover:bg-gray-50" on:click={convertToSoundex(surname)}>Convert</button>
		</div>
		<div>
			<button 
			  on:click={copyToClipboard}
			  class="mt-4 w-full inline-flex text-left rounded-md hover:bg-gray-200 transition bg-gray-100 px-3 py-2 text-sm font-medium text-gray-800">
			  {codedSurname}
			</button>
			<p class="{!copied ? "hidden" : ""} text-sm text-green-600 mt-2 font-bold">Copied Soundex Code!</p>
		</div>
	</div>
</div>

<style>
	#results {
		border: 1px solid #D1D5DB;
	}
</style>