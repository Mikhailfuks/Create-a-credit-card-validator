package main

import ( "fmt","strconv")
)

func main() {
 var cardNumber string
 fmt.Print("Enter credit card number: ")
 fmt.Scanln(&cardNumber)

 if isValid(cardNumber) {
  fmt.Println("Valid credit card number.")
 } else {
  fmt.Println("Invalid credit card number.")
 }
}

// isValid checks if the given credit card number is valid using the Luhn algorithm.
func isValid(cardNumber string) bool {
 // Remove non-digit characters
 cardNumber = cleanCardNumber(cardNumber)

 // Check if the length is valid
 if len(cardNumber) < 13 || len(cardNumber) > 19 {
  return false
 }

 // Reverse the card number
 reversedCardNumber := reverseString(cardNumber)

 // Calculate the Luhn checksum
 sum := 0
 for i, digit := range reversedCardNumber {
  // Convert the digit to an integer
  n, _ := strconv.Atoi(string(digit))

  // Double every other digit
  if (i+1)%2 == 0 {
   n *= 2
  }

  // If doubling results in a two-digit number, subtract 9
  if n > 9 {
   n -= 9
  }

  // Add the digit to the sum
  sum += n
 }

 // Check if the checksum is a multiple of 10
 return sum%10 == 0
}

// cleanCardNumber removes all non-digit characters from the given string.
func cleanCardNumber(cardNumber string) string {
 var cleanCardNumber string
 for _, r := range cardNumber {
  if r >= '0' && r <= '9' {
   cleanCardNumber += string(r)
  }
 }
 return cleanCardNumber
}

// reverseString reverses the given string.
func reverseString(s string) string {
 runes := []rune(s)
 for i, j := 0, len(runes)-1; i < j; i, j = i+1, j-1 {
  runes[i], runes[j] = runes[j], runes[i]
 }
 return string(runes)
}

