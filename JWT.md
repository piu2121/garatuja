```ts
import {type JWTPayload, jwtVerify, SignJWT } from "jose";
const chave_pura=process.env.JWT_SECRET
class Token {
    static  #secret =  new TextEncoder().encode(process.env.JWT_SECRET)
    static async  createJWT(id:string): Promise<string> {
      const jwt = await new SignJWT({userid:id//variavel que vai no payload})
        .setProtectedHeader({ alg: "HS256" }) //algotismo  de hash usado 
        .setIssuedAt()//data que foi criado
        .setExpirationTime("1h") //tempo que expirra
        .setJti(crypto.randomUUID()) //pasar id aleatorio
        .sign(this.#secret);//assinatura
      return jwt;
    }
    
   static async  verifyJWT(token: string): Promise<JWTPayload | null> {
      try {
        const { payload } = await jwtVerify(token, this.#secret);
        console.log("JWT is valid:", payload);
        return payload;
      } catch (error) {
        console.error("Invalid JWT:", error);
        return null;
      }}}
const token = await new SignJWT({ sub: '123456' }) // subject (ID do usuário)
  .setProtectedHeader({ alg: 'HS256' })
  .setIssuer('https://meu-sistema.com')
  .setAudience('https://meu-frontend.com')
  .setExpirationTime('1h')
  //.setNotBefore('5s')     // válido a partir de 5 segundos
  .setIssuedAt()          // agora
  .setJti(crypto.randomUUID()) // ID único
  .sign(secret);

const t=await Token.createJWT('bola')
const a=await Token.verifyJWT(t)
console.log("Created JWT:\n", t,"\n");
console.log("Verified Payload:",a);
```
esse Token serve só pra saber qual usuário fez tal ação,não podendo previnir ataques ###csrf,
pois ele só identifiac o autor,só podendo ser realizado ações por usuários logados.
