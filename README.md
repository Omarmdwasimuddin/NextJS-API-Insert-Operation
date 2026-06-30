## NextJS-API-Insert-Operation

#### prisma.schema
```bash
generator client {
  provider = "prisma-client-js"
  output   = "../app/generated/prisma"
}

datasource db {
  provider = "postgresql"
}

model User {
  id    String     @id @default(uuid())
  email String  @unique
  name  String?
  posts Post[]
}

model Post {
  id        String     @id @default(uuid())
  title     String
  content   String?
  published Boolean @default(false)
  authorId  String
  author    User    @relation(fields: [authorId], references: [id])
}

model Employee {
  id          String @id @default(uuid())
  name        String
  designation String
  city        String
  salary      Int
}
```
---

### Prisma Create() - Insert Single Record
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

### heading...
![](https://imgur.com/EUaBar8.png)

```bash
import { NextRequest, NextResponse } from "next/server";
import prisma from "@/lib/prisma"


export async function POST(request: NextRequest) {
    try {
        
        const json = await request.json();
        
        const employee = await prisma.employee.createMany({
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
