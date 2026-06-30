## NextJS-API-Insert-Operation

![](https://imgur.com/SFPsFff.png)

```bash
import { NextRequest, NextResponse } from "next/server";
import prisma from "@/lib/prisma"


export async function POST(request: NextRequest) {
    try {
        
        const json = await request.json();
        
        const employee = await prisma.employee.create({
            data: json
        })

        return NextResponse.json(
            {status: "success", data: employee},
            {status: 200}
        )
    } catch (error) {
        console.log("Employee insert fail:", error)
        return NextResponse.json(
            {status: "failed", message: "Employee insert fail."},
            {status: 500}
        )
    }
}
```
---
