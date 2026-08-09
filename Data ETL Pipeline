from typing import Any, List, Dict


class QueryBuilder:
    """Lightweight SQL query builder for constructing dynamic database queries."""

    def __init__(self, table_name: str):
        self.table_name = table_name
        self._conditions: List[str] = []
        self._fields: List[str] = ["*"]

    def select(self, *fields: str):
        if fields:
            self._fields = list(fields)
        return self

    def where(self, condition: str):
        self._conditions.append(condition)
        return self

    def build(self) -> str:
        fields_str = ", ".join(self._fields)
        query = f"SELECT {fields_str} FROM {self.table_name}"
        if self._conditions:
            query += " WHERE " + " AND ".join(self._conditions)
        return query + ";"


# Example Usage
if __name__ == "__main__":
    qb = QueryBuilder("policy_holders")
    sql_query = (
        qb.select("id", "first_name", "last_name", "premium_amount")
        .where("status = 'ACTIVE'")
        .where("premium_amount > 500")
        .build()
    )

    print("Generated SQL Query:")
    print(f"  {sql_query}")
