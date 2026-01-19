import { Trophy, Star, Target, MapPin } from "lucide-react"
import { Avatar, AvatarFallback, AvatarImage } from "@/components/ui/avatar"
import { Badge } from "@/components/ui/badge"
import { Card, CardContent, CardHeader } from "@/components/ui/card"

interface UserProfileProps {
  handle: string
  rank: string
  rating: number
  maxRating: number
  contribution: number
  avatarUrl?: string
  organization?: string
  country?: string
}

export function UserProfile({
  handle,
  rank,
  rating,
  maxRating,
  contribution,
  avatarUrl,
  organization,
  country,
}: UserProfileProps) {
  return (
    <Card className="w-full h-full border-border bg-card">
      <CardHeader className="flex flex-row items-center gap-4 pb-4">
        {/* Avatar Section */}
        <Avatar className="h-16 w-16 border-2 border-primary/10">
          <AvatarImage src={avatarUrl} alt={handle} />
          <AvatarFallback className="font-bold">
            {handle.slice(0, 2).toUpperCase()}
          </AvatarFallback>
        </Avatar>

        {/* User Info Section */}
        <div className="flex flex-col gap-1">
          <h2 className="text-2xl font-bold tracking-tight leading-none">
            {handle}
          </h2>
          <Badge 
            variant="outline" 
            className="w-fit capitalize font-medium text-muted-foreground"
          >
            {rank}
          </Badge>
          
          {(organization || country) && (
            <div className="flex items-center text-xs text-muted-foreground mt-1">
              <MapPin className="h-3 w-3 mr-1" />
              <span className="truncate max-w-[200px]">
                {organization && `${organization}, `}{country}
              </span>
            </div>
          )}
        </div>
      </CardHeader>
      
      <CardContent>
        {/* Stats Grid */}
        <div className="grid grid-cols-3 gap-4">
          {/* Current Rating */}
          <div className="flex flex-col gap-1 p-3 rounded-lg bg-secondary/20">
            <span className="text-muted-foreground text-xs flex items-center gap-1.5 font-medium uppercase tracking-wider">
              <Trophy className="h-3.5 w-3.5" /> Rating
            </span>
            <span className="text-xl font-bold">{rating}</span>
          </div>

          {/* Max Rating */}
          <div className="flex flex-col gap-1 p-3 rounded-lg bg-secondary/20">
            <span className="text-muted-foreground text-xs flex items-center gap-1.5 font-medium uppercase tracking-wider">
              <Star className="h-3.5 w-3.5" /> Max
            </span>
            <span className="text-xl font-bold">{maxRating}</span>
          </div>

          {/* Contribution */}
          <div className="flex flex-col gap-1 p-3 rounded-lg bg-secondary/20">
            <span className="text-muted-foreground text-xs flex items-center gap-1.5 font-medium uppercase tracking-wider">
              <Target className="h-3.5 w-3.5" /> Contrib
            </span>
            <span className={`text-xl font-bold ${contribution >= 0 ? 'text-green-500' : 'text-red-500'}`}>
              {contribution > 0 ? `+${contribution}` : contribution}
            </span>
          </div>
        </div>
      </CardContent>
    </Card>
  )
}
