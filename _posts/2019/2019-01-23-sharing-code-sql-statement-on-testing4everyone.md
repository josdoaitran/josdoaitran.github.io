---
layout: post
title:  "Sharing - Code SQL Statement on Testing4Everyone Channels"
author: testing4everyone
categories: [ automation-test, tutorial, document ]
image: assets/images/software-testing-general/testing4everyone-api-testing.png
---

Here is the code, that I shared for API testing in Testing4Everyone.

```java
package utilities;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.SQLException;

public class DatabaseLibs {
    public static void executeStatement(String databaseURL, String user, String password, String statement) {
        Connection conn = null;
        PreparedStatement pstmt = null;

        try {
            conn = DriverManager.getConnection(databaseURL, user, password);
            pstmt = conn.prepareStatement(statement);
            int affectedRows = pstmt.executeUpdate();
            if (affectedRows > 0) {
                System.out.println("Record(s) deleted successfully from statement" + statement);
            } else {
                System.out.println("No records found to delete with the given statement.");
            }
        } catch (SQLException e) {
            System.out.println("Failed to delete record from database: " + e.getMessage());
        } finally {
            try {
                // Close the PreparedStatement and Connection
                if (pstmt != null) {
                    pstmt.close();
                }
                if (conn != null) {
                    conn.close();
                }
            } catch (SQLException e) {
                System.out.println("Failed to close resources: " + e.getMessage());
            }
        }
    }
}
```