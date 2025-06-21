from typing import List
import bisect

class SearchSuggestionSystem:
    def __init__(self, products: List[str]):
        # Sort products lexicographically for binary search
        self.products = sorted(products)

    def getSuggestions(self, searchWord: str) -> List[List[str]]:
        result = []
        prefix = ""
        for char in searchWord:
            prefix += char
            # Find insertion point for prefix using binary search
            i = bisect.bisect_left(self.products, prefix)
            suggestions = []
            # Collect up to 3 matches starting from index i
            for j in range(i, min(i + 3, len(self.products))):
                if self.products[j].startswith(prefix):
                    suggestions.append(self.products[j])
            result.append(suggestions)
        return result
